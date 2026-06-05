Here is the breakdown of your twenty-second transcript. This module is focused on **Cloud Computing Risk, Governance, and Compliance**, a critical knowledge area for the **CompTIA Cloud+** exam and for any professional working in a regulated industry.

### 📝 Crisp Summary
This module covers the unique risks and compliance challenges associated with outsourcing IT services to a cloud provider. It contrasts the centralized, shared-responsibility model of the cloud with traditional on-premises security. The course identifies various business data risks, including the "vendor lock-in" phenomenon, and legal risks related to data sovereignty (e.g., GDPR, HIPAA). It emphasizes the necessity of **Due Diligence** before migrating to the cloud and highlights how a lack of training and the risk of overspending can undermine a cloud strategy. Finally, it outlines how organizations can use a formal **Risk Management Framework (RMF)** to categorize, control, and monitor risks in a constantly evolving cloud environment.

---

### 🎯 MCQ Cheat Sheet (Exam Focus)
*Expect scenario-based questions asking you to identify a specific type of risk (e.g., vendor lock-in) or the appropriate phase of the Risk Management Framework.*

**Cloud Risk Concepts:**
*   **Shared Responsibility Model:** The Cloud Service Provider (CSP) is responsible for the security *of* the cloud (physical data centers, hardware, hypervisor). The customer is responsible for security *in* the cloud (data, IAM configurations, firewalls).
*   **Vendor Lock-In:** A situation where an organization becomes so dependent on a specific cloud provider's proprietary services that the cost and complexity of migrating to a different provider become prohibitive, even if the new provider is better.
*   **Shadow IT:** When employees or departments set up IT systems (like a Dropbox account or a rogue Wi-Fi router) without the knowledge or approval of the central IT department.
*   **Over-Subscribing:** A CSP practice where more virtual resources (vCPUs, RAM) are allocated on a physical host than are actually available, assuming not all customers will use their full allocation at once. This can lead to performance degradation during peak usage.
*   **Due Diligence:** The process of thoroughly investigating a cloud provider's services, compliance reports, and security posture *before* signing a contract.

**The Risk Management Framework (RMF) - 6 Steps:**
1.  **Categorize:** Classify information systems based on their impact level.
2.  **Select:** Choose baseline and supplemental security controls.
3.  **Implement:** Deploy and document the chosen controls.
4.  **Assess:** Evaluate the controls to ensure they are working as intended.
5.  **Authorize:** Formally accept the risk and authorize the system for operation.
6.  **Monitor:** Continuously monitor the controls and the overall framework for effectiveness and changes.

**Legal & Compliance Regulations:**
*   **HIPAA (Health Insurance Portability and Accountability Act):** Protects patient health data in the US.
*   **PCI-DSS (Payment Card Industry Data Security Standard):** Protects credit cardholder data.
*   **GDPR (General Data Protection Regulation):** Protects the data and privacy of EU citizens.
*   **Data Sovereignty:** Laws that mandate certain types of data (e.g., government, citizen data) must physically reside within the borders of a specific country.

**Key ISO Standards:**
*   **ISO 27001:** The international standard for information security management systems.
*   **ISO 27017:** A specific extension of ISO 27001 that provides guidelines for information security controls applicable to the cloud.

---

### 🛠️ Real-World Application (Industry Knowledge)
Here is how you actually deal with Cloud Risk and Compliance in an enterprise environment:

1.  **Avoiding Vendor Lock-In with Containers:** The best way to avoid vendor lock-in is to build your applications in a provider-agnostic way. Instead of using a proprietary service like AWS Lambda, you will build your application to run in **Docker containers orchestrated by Kubernetes**. Since Kubernetes can run on AWS (EKS), Azure (AKS), GCP (GKE), and on-premises, you can easily migrate your entire application workload from one cloud to another with minimal code changes.
2.  **Due Diligence via the CAIQ:** When performing due diligence on a new cloud provider, you don't just ask them random questions. You will send them a formal security questionnaire called the **CAIQ (Consensus Assessments Initiative Questionnaire)** from the Cloud Security Alliance (CSA). Their answers provide a standardized way to evaluate their security posture against industry best practices.
3.  **Fighting "Cloud Wastage":** The video mentions overspending. In a real-world FinOps (Financial Operations) role, you will use tools like **CloudHealth** or **AWS Cost Explorer** to find and shut down "zombie" resources—EC2 instances that a developer spun up for a test three months ago and forgot about, but are still running and costing the company money.
4.  **Enforcing Data Sovereignty with IAM Policies:** If your organization is subject to GDPR, you must ensure that EU citizen data does not leave the EU region. In AWS, you will write an **IAM Service Control Policy (SCP)** at the organization level that explicitly *denies* any user from creating S3 buckets or EC2 instances outside of the `eu-west-1` (Ireland) or `eu-central-1` (Frankfurt) regions.

**You are doing an incredible job. Let's keep the momentum going! Paste the next transcript when you are ready.**