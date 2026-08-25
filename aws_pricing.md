 **comparison format** that is useful for AWS interviews, architecture discussions, and cost-optimization decisions:

| #     | AWS Cost Tool                     | Primary Purpose                      | When to Use             | Key Capability                                                     | Typical Output                        |
| ----- | --------------------------------- | ------------------------------------ | ----------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| **1** | **AWS Pricing Calculator**        | 💰 **Estimate costs**                | **Before deployment**   | Estimate expected AWS costs for new workloads                      | Estimated monthly/annual cost         |
| **2** | **AWS Cost Explorer**             | 📊 **Analyze costs**                 | **After deployment**    | Analyze historical spending and forecast future costs              | Cost trends, usage & forecasts        |
| **3** | **AWS Budgets**                   | 🚨 **Set cost limits**               | **Ongoing**             | Set budgets and trigger alerts/actions when thresholds are reached | Alerts & automated actions            |
| **4** | **AWS Cost & Usage Report (CUR)** | 🗃️ **Detailed billing data**        | **Advanced analytics**  | Provides granular AWS billing and usage data                       | Detailed cost/usage dataset           |
| **5** | **AWS Cost Anomaly Detection**    | 🤖 **Detect unexpected costs**       | **Ongoing monitoring**  | Uses ML to identify unusual spending patterns                      | Anomaly alerts                        |
| **6** | **AWS Cost Optimization Hub**     | 🎯 **Centralize recommendations**    | **Optimization phase**  | Aggregates cost-optimization recommendations across AWS            | Rightsizing & savings recommendations |
| **7** | **AWS Compute Optimizer**         | ⚙️ **Right-size compute**            | **After workloads run** | ML-based recommendations for EC2, Lambda, EBS, ECS, etc.           | Resource sizing recommendations       |
| **8** | **AWS Migration Evaluator**       | ☁️ **Build migration business case** | **Before migration**    | Estimates migration costs and compares on-premises vs AWS          | Migration business case & TCO         |

### 🔑 Easy way to remember

| Stage              | Tool                  | Think of it as                                      |
| ------------------ | --------------------- | --------------------------------------------------- |
| **1️⃣ Plan**       | Pricing Calculator    | **"How much will it cost?"**                        |
| **2️⃣ Analyze**    | Cost Explorer         | **"Where is my money going?"**                      |
| **3️⃣ Control**    | AWS Budgets           | **"Am I exceeding my limit?"**                      |
| **4️⃣ Deep Dive**  | CUR                   | **"Give me all billing details."**                  |
| **5️⃣ Detect**     | Anomaly Detection     | **"Why did my cost suddenly increase?"**            |
| **6️⃣ Optimize**   | Cost Optimization Hub | **"What should I optimize?"**                       |
| **7️⃣ Right-size** | Compute Optimizer     | **"Is my compute oversized?"**                      |
| **8️⃣ Migrate**    | Migration Evaluator   | **"Should we move to AWS, and what will it cost?"** |

### 🎯 Interview shortcut

**Pricing Calculator → Cost Explorer → Budgets → CUR → Anomaly Detection → Optimization Hub → Compute Optimizer → Migration Evaluator**

Think:

> **Estimate → Analyze → Control → Detail → Detect → Optimize → Right-size → Migrate**
