# Windows 11 Client and Domain Join

## Date
September 30 – October 1, 2026

### Objectives
Build a Windows 11 client VM, place it on a shared lab network with the domain controller, join it to the lab.local domain, and verify that the HR-Restrictions GPO applies only to users in the HR Organizational Unit.

### Environment
- Host: Windows 11 (i7-12700H, 16GB RAM)
- Hypervisor: VirtualBox
- DC01: Windows Server 2022 Standard Evaluation, static IP 10.0.2.10
- CLIENT01: Windows 11 Enterprise Evaluation, 4096 MB RAM, 64 GB disk
- Network: VirtualBox NAT Network "LabNet" (10.0.2.0/24)

### What I Did

#### 1. Created a Shared Lab Network
- Opened VirtualBox Network Manager, created NAT Network "LabNet" (10.0.2.0/24, DHCP enabled)
- Shut down DC01, changed Adapter 1 from NAT to NAT Network "LabNet"

#### 2. Assigned DC01 a Static IP
- Set IPv4 address 10.0.2.10, subnet mask 255.255.255.0, gateway 10.0.2.1
- Set preferred DNS to 127.0.0.1 (DC points to itself)
- Verified internet access with ping google.com

#### 3. Built the Windows 11 Client VM
- Created CLIENT01 with 4096 MB RAM, 2 CPUs, EFI enabled, 64 GB disk
- Attached Adapter 1 to NAT Network "LabNet"
- Installed Windows 11 Enterprise, created local account (localadmin) using "Domain join instead"

#### 4. Configured Client DNS
- Set client preferred DNS server to 10.0.2.10 using ncpa.cpl
- Verified with nslookup lab.local, resolved to 10.0.2.10

#### 5. Joined CLIENT01 to the Domain
- System > Domain or workgroup > Change
- Renamed computer to CLIENT01, joined domain lab.local
- Authenticated with Administrator@lab.local
- Received "Welcome to the lab.local domain," restarted

#### 6. Verified GPO Targeting
- Logged in as John Smith (HR): Control Panel and Settings blocked by HR-Restrictions
- Logged in as Mike Jones (IT) and Sarah Davis (Management): Control Panel opened normally
- Took snapshots of DC01 and CLIENT01 as a working baseline

### Key Takeaways
- VMs on plain NAT are isolated from each other; a NAT Network lets them communicate and still reach the internet
- Domain controllers need a static IP, and clients must use the DC as their DNS server to locate the domain
- 10.0.2.3 is VirtualBox's built-in DNS; a client using it cannot find the domain
- nslookup tests DNS directly; ping can fail even when DNS works because Windows Server blocks ICMP by default
- GPOs linked to an OU only affect users in that OU, confirmed by testing users in all three OUs

### Issues / Troubleshooting
1. **"No bootable option found"** on first boot: missed the "Press any key to boot from CD" prompt. Reset the VM and pressed Spacebar immediately.
2. **Client could not find the domain:** client DNS was 10.0.2.3 (VirtualBox default). Manually set DNS to 10.0.2.10 via ncpa.cpl.
3. **nslookup timed out against 10.0.2.10:** DC01 was powered off. Started DC01, waited for AD and DNS services to load, nslookup resolved successfully.
4. **"The specified username is invalid"** during domain join: switched credential format from LAB\Administrator to Administrator@lab.local (UPN format), join succeeded.