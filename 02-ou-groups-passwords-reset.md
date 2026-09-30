# Organizational Units, Groups, Set Passwords, Reset Passwords

## Date
September 29, 2026

### Objectives
Create Organizational Units (such as IT, HR, and Management), Move users into correct units, Create users inside units, Create groups within units and adding members to groups, and reset user passwords.

### Environment
- Host: Windows 11
- Hypervisor: VirtualBox
- VM: Windows Server 2022 Standard Evaluation (Desktop Experience)
- RAM allocated: 4096 MB
- Storage allocated: 60 GB

### What I Did

#### 1. Create Organizational Units
- Opened Server Manager
- Opened Active Directory Users and Computers under tools menu
- Right-Clicked lab.local dropdown menu and opened New Organizational Unit menu
- Created Units IT, HR, and Management with accidental deletion protection enabled

#### 2. Move User into Unit
- Located previously created user John Smith
- Right-clicked user, clicked move option, selected HR

#### 3. Create Users within Units
- Located IT Unit, Right-Clicked, New User
- Created new user: Mike Jones (logon: mjones)
- Located Management Unit, Right-Clicked, New User
- Created new user: Sarah Davis (logon: sdavis)

#### 4. Create Unit Groups and Move Users into Groups
- Located IT Unit, Right-Clicked, New Group
- Created Group (Name: IT-Staff, Scope: Global, Type: Security)
- Double-Clicked IT-Staff Group
- Clicked Members Tab, Add, Typed mjones into object names text box, Clicked check names
- Check names resolved to user Mike Jones
- Clicked OK, Apply, OK
- Mike Jones Successfully added to IT-Staff Group

#### 5. Reset User Password
- Located user John Smith under HR Unit
- Right-Clicked user, Reset Password
- Typed new password, checked "Unlock the user's account", Clicked OK
- New Password set successful

### Key Takeaways
- Creating units and groups helps keep order within the user directory of the Organization
- Moving users is very simple in case a user is created outside of a unit or group or roles change within the Organization.
- Security groups control permissions for multiple users at once
- Disabled accounts show a down arrow icon in ADUC — quick visual indicator of account status
- Resetting a password and unlocking an account can be done in one step — always check "Unlock the user's account" when resetting

### Issues / Troubleshooting
No issues