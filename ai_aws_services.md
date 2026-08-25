### Amazon SageMaker
What it's for: Build/train/deploy custom ML models (fraud detection, credit scoring, algo trading signals).

**Pros**: Full control over model architecture — important when regulators want explainability; supports built-in algorithms for fraud/anomaly detection; SageMaker Clarify helps with bias detection and explainability (useful for fair lending compliance); integrates with Model Monitor for drift detection, which examiners like to see.

**Cons**: Steep learning curve and higher operational overhead than managed APIs; cost can balloon with large training jobs and always-on endpoints; you own the compliance burden for model validation (SR 11-7 style model risk management) since it's not a black-box managed service.

### Amazon Fraud Detector

**What it's for:** Purpose-built for real-time transaction fraud, account takeover, and new-account fraud.

**Pros**: Pre-trained fraud-specific models mean faster time-to-value than building from scratch; low-latency real-time scoring API fits payment authorization flows; pay-per-prediction pricing scales with transaction volume.

**Cons**: Less flexible than a custom model — harder to tune for niche fraud patterns; limited explainability compared to a self-built model with SHAP values; being deprecated/limited in newer AWS roadmaps in favor of SageMaker-based approaches, so check current service status before committing long-term.

### Amazon Comprehend / Comprehend Medical

**What it's for:** NLP for document processing — KYC document analysis, contract review, sentiment on customer complaints, entity extraction from financial filings.

**Pros**: Good for extracting entities (names, amounts, dates) from unstructured text like loan applications; PII detection API helps with data governance; no ML expertise required.

**Cons**: Generic NLP models may underperform on dense financial/legal jargon vs. a fine-tuned LLM; not built for structured financial documents (tables, forms) — that's more Textract's job.

### Amazon Textract

**What it's for:** OCR + structured data extraction from documents — pay stubs, tax forms, bank statements, loan applications.

**Pros**: Strong at extracting tables and key-value pairs (critical for underwriting docs); AnalyzeID feature specifically handles driver's licenses/passports for KYC; reduces manual data entry significantly.

**Cons**: Accuracy drops on poor-quality scans or non-standard document formats; per-page pricing adds up at high volume; still needs human-in-the-loop review for regulatory-grade accuracy.

### Amazon Bedrock

**What it's for**: Access to foundation models (Claude, Titan, others) for chatbots, document summarization, research assistants, code generation.

**Pros**: No infrastructure management; choice of multiple model providers; data stays within your AWS environment/VPC (important for data residency requirements); Guardrails feature helps filter outputs for compliance-sensitive use cases.

**Cons**: LLM hallucination risk is a real problem in regulated contexts (e.g., generating inaccurate financial advice); still maturing around auditability of model decisions; token-based pricing can be unpredictable at scale; foundation models aren't inherently trained on your institution's specific regulatory environment.

### Amazon Lex

**What it's for**: Conversational AI for customer service chatbots/IVR (balance inquiries, card blocking, basic support).

**Pros**: Deep integration with Connect (contact centers) already used by many banks; handles both voice and text; built-in intent recognition reduces dev time for common banking FAQs.

**Cons**: Struggles with complex, multi-turn financial queries without heavy customization; still needs escalation paths to human agents for anything account-specific or emotionally sensitive; newer Bedrock-based agents are arguably outpacing Lex for sophisticated use cases.

### Amazon Macie

**What it's for**: Sensitive data discovery and classification in S3 (PII, PCI data, account numbers).

**Pros**: Automated scanning helps meet PCI-DSS and data privacy audit requirements; useful for finding sensitive data sprawl before a breach, not after.

**Cons**: S3-only scope — doesn't cover data in RDS, on-prem, or other stores; can generate false positives requiring tuning; another line item cost on top of storage.

### Fintech-specific cutting concerns across all of these
**Explainability/auditability**: Regulators (OCC, CFPB, EU's AI Act if you're in Europe) increasingly expect model decisions to be explainable — custom SageMaker models with Clarify tend to satisfy this better than black-box managed APIs.

**Data residency & encryption**: Check which services support VPC-only deployment and encryption-at-rest/in-transit by default — not all AWS AI services are equal here.

**Compliance certifications**: Confirm SOC 2, PCI-DSS scope, and (if relevant) FedRAMP status per service before architecting around it — coverage varies service to service.

**Vendor lock-in**: Heavy reliance on AWS-specific APIs (like Fraud Detector's proprietary models) can make it harder to switch providers or bring processing in-house later.
