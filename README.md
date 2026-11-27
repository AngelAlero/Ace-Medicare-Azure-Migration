# Healthcare Cloud Migration Project: Mapping Ace Medicare Clinics On-Premises Scenarios to Microsoft Azure

## Project Summary & Tasks Completed
In this project, I acted as a Cloud Solutions Architect to plan the migration of **Ace Medicare Clinics** from an aging on-premises server room to **Microsoft Azure**. Specifically, I completed the following tasks:
1. **Workload Assessment:** Evaluated 5 real-world clinical IT workloads (Electronic Health Records, Patient Portal, SQL Database, Radiology Imaging, and Staff Email) for cloud readiness.
2. **Migration Mapping (The 5 Rs):** Mapped each on-premises scenario to an appropriate Azure cloud service using Rehost, Refactor, Rearchitect, and Replace strategies.
3. **Financial & TCO Analysis:** Built a 3-year Total Cost of Ownership (TCO) comparison evaluating CapEx vs. OpEx spending (detailed in `tco-calculation-sheet.txt`).
4. **Compliance & Cost Optimization:** Designed a HIPAA/NDPR security architecture and a post-migration governance roadmap (detailed in `optimization-roadmap.txt`).

---

## 1. Core Azure Fundamentals: CapEx vs. OpEx & Shared Responsibility
Ace Medicare Clinics currently runs 16 physical servers inside its main facility server room (on-premises). Because these servers are 5 years old, the organization faces an immediate **$240,000** hardware replacement cost.

* **Capital Expenditure (CapEx - On-Premises Model):** CapEx requires spending large sums of money upfront to buy physical servers, storage hard drives, and networking gear. Ace Medicare Clinics bears 100% of the risk if hardware breaks or sits idle at night.
* **Operating Expenditure (OpEx - Azure Cloud Model):** OpEx means renting computing power from Microsoft Azure over the internet with zero upfront hardware purchase. Ace Medicare Clinics pays a predictable monthly bill based on actual usage, shifting IT from a fixed capital burden to an agile operating expense.
* **Azure Shared Responsibility Model:** On-premises, the clinic IT team manages everything from physical building locks and air conditioning to software patches. In Azure, Microsoft manages physical data center security, hardware failures, and host networking, while Ace Medicare Clinics manages patient data security, user access, and application configuration.

---

## 2. Detailed On-Premises Scenarios & Azure Service Mapping (The 5 Rs)

### Scenario 1: Main Electronic Health Record (EHR) System
* **On-Premises Setup:** Doctors and nurses use a legacy Windows Server 2016 desktop/backend application to view patient histories and prescriptions. The vendor no longer supports code modifications.
* **Assigned Strategy (Rehost / Lift & Shift):** Moving an existing server directly to the cloud without modifying application code.
* **Mapped Azure Service:** **Azure Virtual Machines (IaaS - Infrastructure as a Service)**
* **How the Azure Service Works & Use Case:** Azure Virtual Machines provide on-demand, scalable virtualized servers hosted in Microsoft data centers. By rehosting the EHR system onto memory-optimized Azure VMs (E-series), Ace Medicare Clinics eliminates failing on-site hardware immediately with zero code changes while gaining automated backups and disaster recovery via **Azure Site Recovery**.

### Scenario 2: Patient Appointment Booking and Lab Results Portal
* **On-Premises Setup:** Patients log into an ASP.NET web portal hosted on a local IIS web server. Heavy Monday morning traffic (8:00 AM – 11:00 AM) frequently overwhelms the local server and causes slowdowns.
* **Assigned Strategy (Refactor):** Making minor configuration adjustments so an application runs on a managed cloud platform without rewriting core code.
* **Mapped Azure Service:** **Azure App Service (PaaS - Platform as a Service)**
* **How the Azure Service Works & Use Case:** Azure App Service is a fully managed web hosting platform where Microsoft handles OS patching, security updates, and load balancing. Hosting the patient portal on Azure App Service enables **Autoscaling**, automatically adding compute power during busy Monday mornings and scaling down at night to save costs.

### Scenario 3: Core Patient Records and Billing Database
* **On-Premises Setup:** 4 TB of structured patient demographics, insurance claims, and billing records sit on a local Microsoft SQL Server 2019 Enterprise server, requiring 15 hours/week of manual database administration.
* **Assigned Strategy (Refactor):** Migrating the database to a managed cloud database engine while preserving existing SQL schemas and queries.
* **Mapped Azure Service:** **Azure SQL Managed Instance (PaaS)**
* **How the Azure Service Works & Use Case:** Azure SQL Managed Instance provides near-100% compatibility with on-premises SQL Server while automating backups, high availability, and patching. Clinical apps continue querying patient records seamlessly while Azure maintains encrypted point-in-time backups every 5 minutes.

### Scenario 4: Radiology X-Ray, CT, and MRI Image Archive
* **On-Premises Setup:** The radiology department stores 50 TB of large medical imaging files (DICOM format) on local Storage Area Network (SAN) disks that are 95% full.
* **Assigned Strategy (Rearchitect):** Redesigning data storage architecture to leverage cloud-native APIs and tiered object storage.
* **Mapped Azure Services:** **Azure Health Data Services (DICOM Service)** + **Azure Blob Storage**
* **How the Azure Service Works & Use Case:** Azure Health Data Services natively ingests and manages medical imaging using standard DICOM protocols, backed by Azure Blob Storage. New X-rays stay in the fast **Hot Tier** for instant doctor viewing, automatically move to the **Cool Tier** after 90 days, and shift to the low-cost **Archive Tier** after 1 year to satisfy 7-year legal retention laws affordably.

### Scenario 5: Clinic Staff Email and Clinical Messaging
* **On-Premises Setup:** 800 doctors, nurses, and staff across Ace Medicare Clinics use an aging on-premises Microsoft Exchange 2016 email server that suffers downtime whenever local power fluctuates.
* **Assigned Strategy (Replace):** Retiring an in-house server and adopting a commercial Software-as-a-Service (SaaS) solution.
* **Mapped Cloud Service:** **Microsoft 365 (Exchange Online & Microsoft Teams - SaaS)**
* **How the Azure Service Works & Use Case:** Microsoft 365 delivers fully managed enterprise email and collaboration over the internet with a 99.9% uptime SLA, eliminating physical server maintenance while giving clinic staff encrypted email and HIPAA-compliant Teams chat.

---

## 3. Healthcare Compliance (HIPAA & NDPR) and Security Architecture
Because Ace Medicare Clinics processes Protected Health Information (PHI), the Azure architecture enforces strict privacy and security controls under **HIPAA** and **NDPR**:
* **HIPAA Business Associate Agreement (BAA):** Executing Microsoft’s BAA legally guarantees that covered Azure services meet healthcare data protection standards.
* **Azure Key Vault & Encryption:** All databases and Blob storage enforce **AES-256 encryption at rest** and **TLS 1.2+ encryption in transit**, with encryption keys secured inside hardware-backed **Azure Key Vault**.
* **Azure Virtual Network (VNet) & Private Endpoints:** Patient databases are placed inside an isolated private VNet with public internet access disabled, reachable only via an encrypted **Azure VPN Gateway**.
* **Microsoft Entra ID:** Enforces Multi-Factor Authentication (MFA) and Role-Based Access Control (RBAC) so staff only access records permitted for their clinical role.
* **Microsoft Defender for Cloud:** Continuously audits Azure resources against the built-in **HIPAA / HITRUST** compliance standard and alerts IT administrators to any security misconfiguration.

---

## 4. Sustainability and Hybrid Cloud Boundaries
* **Sustainability Impact:** Consolidating 16 local servers and 24/7 air conditioning onto Microsoft’s renewable-energy data centers reduces Ace Medicare Clinics’ IT carbon footprint by **~74%**.
* **When On-Premises Remains Better:** Real-time **urgent care patient monitors** and **diagnostic imaging acquisition terminals** require zero-latency local operation even if external internet fails. These remain on-premises and are governed centrally through **Azure Arc**.

