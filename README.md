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

*   **Infrastructure (VirtualBox Manager):** Hosts the Windows Server **Domain Controller (DFIR.local)**, a **Windows Test Machine**, and a **Splunk Server** (Ubuntu).
*   **Attack Vector:** An external attacker authenticates to the publicly exposed **Test Machine**; successful login telemetry is immediately forwarded to **Splunk**.
*   **Detection & Notification:** **Splunk** triggers an alert, sending a notification to **Slack** and a webhook to the **Shuffle SOAR** platform.
*   **Automated Response:** The **"Successful Unauthorized Login Playbook"** emails a **SOC Analyst** to approve or deny an account lockout.
*   **Remediation:** If approved, **Shuffle** instructs the **DC** to disable the domain user and logs the final status to **Slack**.
