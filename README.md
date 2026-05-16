# Active Directory Project

## Part 1: Logical Diagram

### Objective
Create an Active Directory environment in Draw.io, integrating all core components and their connectivity so I can automate responsive actions.

### Skills Learned
- Active Directory architecture design
- SIEM integration planning (Splunk)
- SOAR workflow mapping (Shuffle)
- Security telemetry flow design
- Infrastructure visualization using Draw.io

### Tools
- Draw.io

### Steps

Ref 1: Network Diagram  
<img src="diagram-part1.png">

### Summary of Components & Telemetry Flow

* **Infrastructure (VirtualBox Manager):** Hosts the Windows Server **Domain Controller**, a **Windows Test Machine**, and a **Splunk Server** (Ubuntu).
* **Attack Vector:** An external attacker authenticates to the publicly exposed **Test Machine**; successful login telemetry is immediately forwarded to **Splunk**.
* **Detection & Notification:** **Splunk** triggers an alert, sending a notification to **Slack** and a webhook to the **Shuffle SOAR** platform.
* **Automated Response:** The **"Successful Unauthorized Login Playbook"** emails a **SOC Analyst** to approve or deny an account lockout.
* **Remediation:** If approved, **Shuffle** instructs the **DC** to disable the domain user and logs the final status to **Slack**.

---

# Part 2: Infrastructure Deployment & Network Validation

## Objective
- Install 3 VMs in VirtualBox Manager which acts as my cloud. 
- Test communication: Implement a dual-adapter network configuration (NAT + Host-Only) across all VMs to enable external internet access and isolated internal communication within a controlled environment.

### Skills Learned
- Virtual machine provisioning and resource allocation in VirtualBox.
- Dual-network architecture (NAT + Host-Only) design, implementation, and connectivity validation.
- Remote administration via SSH for Linux-based security servers.
- Network interface analysis using ip a and ipconfig across different OSs.
- Multi-VM environment preparation for AD, SIEM, and workstation integration.

### Tools
- Oracle VM VirtualBox Manager (Hypervisor)
- Windows Server 2022 (Domain Controller)
- Windows 10 (Workstation)
- Ubuntu Server 24.04 LTS (Splunk Host)
- OpenSSH (Remote Administration)
- PowerShell (Windows Connectivity Testing)
- Bash (Linux Connectivity Testing)

### Steps

Ref 1: Oracle VM VirtualBox Manager (Home Interface)  
This view displays the initial VirtualBox dashboard and environment preparation.
<img src="screenshots-part2/vBox-manager.png">

Ref 2: Virtual Machine Configuration Overview  
A consolidated overview of the Windows Server (Domain Controller), Windows 10 Workstation, and Ubuntu Splunk Server virtual machines, including configured specifications, roles, and resource allocations displayed in the right pane.
<img src="screenshots-part2/Win-server.png">

Ref 3: Ubuntu Network Interface Verification (Dual NIC Setup)  
Confirmation of the dual-adapter setup using `ip a` to ensure both NAT and Host-Only connectivity.
<img src="screenshots-part2/ubuntu-dual-ip.png">

Ref 4: Remote Administration & External Connectivity  
Demonstration of successful SSH access and external reachability to 8.8.8.8.
<img src="screenshots-part2/uduntu-connectivity.png">

Ref 5: Internal Connectivity Test (ICMP)  
Successful internal ping between the Windows Workstation and the Domain Controller confirming subnet alignment.
<img src="screenshots-part2/win-winserver-ping.png">

---

# Part 3: Active Directory Domain Services & Client Integration

### Objective
Install and configure Active Directory Domain Services, promote the Windows Server to a Domain Controller, and join a Windows 11 test machine to the domain DFIR.local.

### Skills Learned
- Active Directory Domain Services (AD DS) installation and Domain Controller promotion.
- DNS configuration and client-server identity resolution.
- Windows workstation domain join and user authentication.
- User account and object management within Active Directory Users and Computers (ADUC).

### Tools
- Windows Server (Active Directory Domain Services)
- Windows 11 Pro VM (Test machine)
- Active Directory Users and Computers (ADUC)
- DNS Manager
- Oracle VM VirtualBox (Environment)

### Steps

Ref 1: Domain Controller Promotion
AD DS and DNS roles installed and domain controller promotion completed successfully.
<img src="screenshots-part3/01_AD_Promote_DC.png">

Ref 2: Active Directory Object Creation
ADUC showing DFIR.local domain with new user “Dele Smith” created (left pane).
<img src="screenshots-part3/02_ADUC_User_Created.png">

Ref 3: Workstation Domain Join
Windows 11 VM successfully joined to DFIR.local domain and authenticated using domain credentials.
<img src="screenshots-part3/03_testPC_AD_join.png">

Ref 4: Active Directory Client Verification
Windows 11 machine successfully registered in Active Directory under DFIR.local Computers container.
<img src="screenshots-part3/04_ADUC_TargetPC.png">

