Here is the breakdown of your eleventh transcript. This module moves into the highly practical and operational side of cybersecurity: **Data Access Governance (DAG)**. It covers everything from classifying data to encrypting it and actively auditing it in a Microsoft Windows Server environment.

### 📝 Crisp Summary
This module focuses on the principles of **Data Access Governance**. The process begins with **Data Classification** (tagging data as Internal, Sensitive, or Public) to determine how it must be protected. Next, it covers protecting data at rest using **BitLocker** or **EFS (Encrypting File System)** and protecting data in transit using **VPNs**. Finally, it demonstrates how to enforce and monitor these rules using Microsoft's System Center Configuration Manager (SCCM), Windows Event Viewer (for auditing and filtering logs), and SIEM systems to conduct large-scale Data Analytics.

---

### 🎯 MCQ Cheat Sheet (Exam Focus)
*You are highly likely to see questions on the differences between BitLocker and EFS, as well as questions on Event IDs and asymmetric/symmetric encryption.*

**Data Classification Types:**
*   **Public:** Product catalogs, marketing materials, bus routes.
*   **Internal:** Org charts, budgets, employee onboarding docs.
*   **Sensitive:** PHI (Personal Health Information), PII (Personally Identifiable Information), financial data. *Often restricted from cloud storage due to Data Sovereignty laws.*

**Encryption Concepts:**
*   **Symmetric Encryption:** Uses *one* secret key to both encrypt and decrypt (e.g., AES). Fast, but hard to distribute the key securely.
*   **Asymmetric Encryption:** Uses *two* mathematically related keys (Public and Private). 
    *   *Rule of thumb:* To encrypt a message for Bob, you use **Bob's Public Key**. Bob decrypts it with **his Private Key**.
*   **BitLocker:** Encrypts the *entire disk volume*. Can be used on the OS drive (requires a TPM chip) or a removable USB drive (BitLocker To Go).
*   **EFS (Encrypting File System):** Encrypts *individual files or folders*. Tied to the specific user account that encrypted it.

**Regulations & Compliance:**
*   **PCI-DSS:** Payment Card Industry Data Security Standard (Credit card data).
*   **HIPAA:** Health Insurance Portability and Accountability Act (US Medical data).
*   **GDPR:** General Data Protection Regulation (European Union data privacy).
*   **PIPEDA:** Personal Information Protection and Electronic Documents Act (Canadian privacy law).

**Auditing & Logging:**
*   **Windows Event Viewer:** Central tool for viewing logs. Security audits (like successful or failed logins) are found in the **Security Log**.
*   *Key Event ID:* **4648** indicates a successful logon audit event.
*   **SIEM (Security Information and Event Management):** A centralized system that ingests logs from all servers/firewalls, correlates the data, and provides real-time alerts for abnormal behavior.

---

### 🛠️ Real-World Application (Industry Knowledge)
Here is how this translates directly to your day-to-day job as a Systems Administrator or Security Analyst:

1.  **Deploying Microsoft FSRM (File Server Resource Manager):** You will rarely classify files manually. As shown in the video, you will use FSRM to scan massive corporate file shares. You will set a regular expression (regex) rule to look for Social Security Numbers (e.g., `\d{3}-\d{2}-\d{4}`). If FSRM finds a match in a Word doc, it will automatically tag the file as "Highly Sensitive PII," which then triggers your Data Loss Prevention (DLP) agent to block anyone from emailing that file outside the company.
2.  **BitLocker Recovery Keys in AD:** When you deploy BitLocker to 500 company laptops, you won't save the recovery keys to a text file on a USB stick (as shown in the simplified demo). You will configure **Group Policy (GPO)** to automatically back up every single laptop's BitLocker Recovery Key directly into **Active Directory (AD)**. If a user gets locked out, the Helpdesk can look up the key in AD.
3.  **Reducing Audit Noise:** The video highlights a massive real-world problem: "Audit Noise." If you turn on "Audit File System" in Group Policy for *every* file, your servers will generate millions of log entries an hour, crashing your SIEM. You must only configure auditing on high-risk folders (like the HR drive or Financials) and only audit specific events (e.g., auditing *Failures* to read files, rather than every successful read). 
4.  **VPNs and Split Tunneling:** When configuring a VPN (like the PPTP demo, though in modern infra you will use more secure IPsec or OpenVPN), you will often have to decide on **Split Tunneling**. Do you want the remote user's Netflix traffic to route through your corporate VPN (slowing down your network), or do you only want traffic destined for `10.x.x.x` (corporate resources) to go through the tunnel?

**We are flying through these. Paste the next one whenever you're ready!**