# Group Policy Basics

## Date
September 30, 2026

## Objectives
Take snapshot of VM for backup precautions, Configure minimum password length and account lockout policies via Default Domain Policy, Test policy changes, Create and link HR-Restriction Group Policy Object (GPO)

## Environment
No Change

## What I Did

### 1. Take VM Snapshot
- Opened VirtualBox
- L-Click on Snapshots Menu
- L-Click Take Snapshot, Named Snapshot: 09302026 Pre-GPO, L-Click OK
- Saved Successfully

### 2. Configure Default Domain Policies
- Booted DC01, Login as Admin
- Opened Server Manager
- L-Click Tools, Group Policy Management
- Expanded Forest: lab.local > Domains > lab.local
- R-Click Default Domain Policy > Edit
- Expanded Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > L-Click on Password Policy
- Dbl-Click Minimum Password Length, Set to 10 characters, OK
- Under Account Lockout Policy, Dbl-Click Account Lockout Threshold, Set to 5 attempts
- Closed Group Policy Management Editor, Forced update via Command Prompt using gpupdate /force
- Tested policy changes, Results are successful

### 3. Create Unit Specific GPO
- Opened Group Policy Management under tools menu
- R-Click HR Organization Unit > Create a GPO in this domain, and Link it here...
- Named: HR-Restrictions > OK
- R-Click HR-Restrictions > Edit
- Under User Configuration, Expand Policies > Administrative Template > L-Click Control Panel
- Dbl-Click Prohibit access to Control Panel and PC settings
- Select Enabled > OK
- Closed editor and ran gpupdate /force

## Key Takeaways
- Taking snapshots before making big changes offers a valuable "Do Over" button just in case a system breaking mistake is made
- Default Domain Policies is system wide for every user, GPO's linked to a unit applies only to that unit; Such as a GPO for HR doesnt apply to IT or Management
- gpupdate /force applies policy changes immediately instead of the default refresh cycle
- User Configuration is for specific users no matter what computer they sign into, Computer Configuration applies to that specific machine no matter who logs in

## Issues / Troubleshooting
No issues