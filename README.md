Healthcare Cloud Migration Project: Moving Ace Medicare Clinics to Microsoft Azure
1. Project Overview and Why We Are Moving (CapEx vs. OpEx)
Ace Medicare Clinics currently runs all its patient records, X-ray storage, and staff email on physical servers inside its own building (on-premises). Those servers are 5 years old and need to be replaced soon.
•	Staying On-Premises (CapEx - Capital Expenditure): Buying new physical servers and storage drives requires paying $240,000 upfront, plus ongoing bills for electricity, cooling, and hardware repairs.
•	Moving to Microsoft Azure (OpEx - Operating Expenditure): Instead of buying hardware, the hospital rents computing power from Microsoft Azure and pays a predictable monthly bill based on what it uses.
By moving to Azure and applying smart cost-saving discounts, Ace Medicare Clinics will save $212,000 (38.5%) over 3 years while keeping patient data safer and more reliable.
2. Hospital Workloads and How We Will Move Them (The 5 Rs)
Before moving anything, I reviewed the 5 main IT systems the hospital currently uses and matched each one to the best migration strategy:
•	System 1: Main Hospital Record System (EHR)
o	Current Setup: Old Windows Server 2016 desktop and backend app.
o	Migration Strategy: Rehost (Lift and Shift).
o	New Azure Service: Azure Virtual Machines.
o	Why This Choice Makes Sense: The software vendor no longer updates this app, so we cannot rewrite the code. Moving it as-is to an Azure VM gets us off old hardware safely with low risk.
•	System 2: Patient Appointment and Lab Portal
o	Current Setup: Local web server running a .NET web app.
o	Migration Strategy: Refactor.
o	New Azure Service: Azure App Service.
o	Why This Choice Makes Sense: With a few small configuration tweaks, Azure handles server updates automatically and scales up when many patients book appointments in the morning.
•	System 3: Patient Database
o	Current Setup: Microsoft SQL Server 2019 holding 4 TB of patient files.
o	Migration Strategy: Refactor.
o	New Azure Service: Azure SQL Managed Instance.
o	Why This Choice Makes Sense: It works just like our current SQL database, but Microsoft automatically handles backups, security patches, and crash recovery.
•	System 4: X-Ray and MRI Image Storage
o	Current Setup: Local hard drive storage holding 50 TB of medical scans.
o	Migration Strategy: Rearchitect.
o	New Azure Service: Azure Health Data Services and Azure Blob Storage.
o	Why This Choice Makes Sense: Instead of buying expensive local hard drives every year, recent scans stay on fast storage while older scans move to cheap long-term cloud storage.
•	System 5: Staff Email and Messaging
o	Current Setup: On-site Exchange 2016 email server for 800 staff members.
o	Migration Strategy: Replace.
o	New Azure Service: Microsoft 365 (Exchange Online and Teams).
o	Why This Choice Makes Sense: Running an email server is hard work. Switching to Microsoft 365 gives doctors and nurses secure email and chat immediately with zero server maintenance.
3. Healthcare Compliance and Patient Data Security
Because hospitals store private medical records (Protected Health Information / PHI), we must follow strict healthcare privacy laws—specifically HIPAA (international healthcare standard) and NDPR (Nigeria Data Protection Regulation). Here is how we keep patient data legal and secure on Azure:
•	Legal Agreement (HIPAA BAA): Ace Medicare Clinics will sign Microsoft’s official Business Associate Agreement (BAA), which legally guarantees that Microsoft’s cloud tools meet healthcare privacy rules.
•	Data Encryption (Locking the Data): All patient records and X-rays are automatically encrypted using AES-256 encryption while stored, and TLS encryption while traveling over the internet. Encryption keys are safely locked inside Azure Key Vault.
•	Private Network Only: Patient databases will be placed inside a private Azure Virtual Network (VNet) with no public internet access, blocking outside hackers from reaching them.
•	Strict Staff Login Rules: Using Microsoft Entra ID, every doctor, nurse, and admin must use Multi-Factor Authentication (MFA) and only gets access to the specific files needed for their job.
•	24/7 Security Monitoring: We will turn on Microsoft Defender for Cloud with the HIPAA security checklist enabled. It automatically alerts our IT team if any setting is unsafe and saves activity logs for the legally required 6+ years.
4. Environmental Impact and When Staying On-Premises Makes Sense
•	Greener IT (Sustainability): Running 16 physical servers and 24/7 air conditioning in the hospital wastes a lot of electricity. Moving to Microsoft’s energy-efficient data centers cuts the hospital’s IT carbon footprint by about 74%.
•	When On-Premises is Still Better: Not everything belongs in the cloud. Machines inside the hospital that need instant, zero-delay responses—like live operating room monitors or local MRI scanner buffers—should stay on-site so they still work even if the internet goes down. We can connect them to Azure safely using Azure Arc.
