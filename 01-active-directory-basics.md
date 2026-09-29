# Active Directory Basics

## Date
September 28, 2026

### Objective
Install Active Directory Domain Services on Windows Server 2022 
and perform basic user account management tasks.

### Environment
- Host: Windows 11 (Gaming Laptop)
- Hypervisor: VirtualBox
- VM: Windows Server 2022 Standard Evaluation (Desktop Experience)
- RAM allocated: 4096 MB
- Storage allocated: 60 GB

### What I Did

#### 1. Installed VirtualBox and Windows Server 2022
- Downloaded VirtualBox for Windows and installed it
- Created a new VM (DC01) with 4GB RAM, 2 CPUs, 60GB disk
- Mounted Windows Server 2022 ISO and completed installation
- Set Administrator password and logged in

#### 2. Installed Active Directory Domain Services
- Opened Server Manager
- Added the Active Directory Domain Services role
- Clicked "Promote this server to a domain controller"
- Created a new forest with root domain: lab.local
- Server rebooted and came back as LAB\Administrator

#### 3. User Account Management
- Opened Active Directory Users and Computers (Tools menu)
- Created new user: John Smith (logon: jsmith) in the Users OU
- Disabled the account — noticed the down arrow icon on the account
- Re-enabled the account

### Key Takeaways
- Disabled accounts show a down arrow icon in ADUC
- Domain login format is DOMAIN\username (LAB\Administrator)
- Server Manager is the central dashboard for all Windows Server roles
- DSRM password is a recovery password separate from Administrator

### Issues / Troubleshooting
None — clean install.