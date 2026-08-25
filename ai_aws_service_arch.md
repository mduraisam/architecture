
<img width="1078" height="978" alt="image" src="https://github.com/user-attachments/assets/9f2efb85-d7e7-41da-93e1-f22d070c4458" />


### How it fits together

### Ingestion layer
API Gateway + Lambda front every channel (app, call center, document upload) — this is where you enforce auth, rate limiting, and route events to the right service by type. Lambda functions are stateless glue: they don't run models themselves, just orchestrate calls to the AI layer below.

### KYC / onboarding lane
Uploaded IDs, pay stubs, and bank statements hit Textract's AnalyzeID and forms/tables extraction first. Anything with free-text (loan narratives, employment letters) goes through Comprehend for PII detection and entity extraction before it's allowed to touch the data lake. This is the lane where you want the most human-in-the-loop review — treat model output as a draft, not a decision.

### Real-time fraud lane
Fraud Detector handles the first-pass scoring on transaction/payment events since it's low-latency and purpose-built. Route flagged or high-value transactions to a custom SageMaker endpoint for a second opinion — this two-tier setup gives you speed on the easy 95% and explainability/control on the cases that actually get escalated or disputed.

### Conversational lane
Lex handles intent-based banking FAQs (balance, card block, branch hours) since it's cheap and deterministic. Anything Lex can't resolve — multi-turn reasoning, document summarization, "explain my statement" — escalates to Bedrock (Claude), with Guardrails configured to block financial-advice-sounding outputs unless that's an explicit, compliance-reviewed use case.

### Data + governance layer
Everything lands in an S3 data lake. Macie continuously scans for PII/PCI exposure. SageMaker Clarify runs bias and feature-attribution checks on the fraud/credit models specifically — this is your fair-lending evidence. Model Monitor watches for drift so a model that was compliant at launch doesn't quietly become discriminatory six months later as transaction patterns shift.

### Audit layer
Every AI decision (accept/reject, fraud score, chatbot escalation) needs to be logged with the model version and input that produced it — CloudTrail plus a dedicated compliance dashboard (QuickSight or similar) is what you hand an examiner when they ask "why was this loan denied."

### A few build notes:

### VPC everything
Bedrock and SageMaker should run with VPC endpoints so payloads never traverse the public internet — expect this to come up in any vendor risk review.
### Don't let Bedrock touch account-level actions directly
Use it for drafting/summarizing/answering, but route any actual money-movement or account change through your existing transactional systems with normal auth checks — LLMs shouldn't be an unaudited path to state changes.
### Fraud Detector vs. SageMaker isn't either/or
Cheap fast model catches the obvious cases; custom model handles the ones worth the extra compute and gives you a defensible explanation trail for disputes.
