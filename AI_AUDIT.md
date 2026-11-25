# AI Automation & Code Audit Log

> **Student Name:** [Allan]  
> **Student ID:** [W0520390]  
> **AI Tool Used:** [Microsoft 265 copilot]  

---

## 1. Executive Summary
AI was used as an infrastructure engineering assistant to analyze the OSYS3030 appliance configuration files and Markdown
documentation, then generate deployment and verification Bash scripts.
The generated scripts were manually reviewed, tested on VM 115, debugged,
and corrected to match the appliance configuration. Human review was required 
to identify verification errors, privilege issues, and appliance-specific settings before the scripts achieved a successful verification result.

---

## 2. Prompt Log

### 2.1 Deployment Script Prompt the exact prompt you gave the AI to generate
deploy_appliance.sh.sample
```
povided verify_applicane.sh.sample script, modified and auited with microsoft 265 copilot..... deploy_appliance.sh.sample
```

### 2.2 Verification Script Prompt
Paste the exact prompt you gave the AI to generate `verify_appliance.sh`:
verify_appliance.sh.sample
```
verify_appliance.sh.sample
```

---

## 3. Human-in-the-Loop Audit & Hallucination Corrections

AI models frequently introduce errors when writing infrastructure automation. Document at least 2 specific errors, bugs, or omissions the AI made in the generated scripts and how you fixed them:

| # | Service / Component | The AI's Hallucination / Error | The Fix Implemented|
|---|---------------------|--------------------------------|--------------------|
| 1 | OpenSSH Verification | Verification script checked SSH on TCP port 22 even though the appliance was configured to use TCP port 2222. | Updated verify_appliance.sh to validate TCP port 2222. |
| 2 | Kea DHCP Verification | DHCP verification produced a false failure because the original validation logic did not correctly verify the Kea configuration in the appliance environment. | Updated the verification logic to correctly validate the Kea configuration file. |
| 3 | UFW Firewall Verification | Firewall verification reported a failure even though UFW was active and functioning correctly. | Updated the verification command to use elevated privileges when checking firewall status. |
| 4 | NAT Verification | NAT verification reported a failure even though a MASQUERADE rule existed in the NAT table. | Updated the verification command to use elevated privileges when checking iptables NAT rules. |
| 5 | Deployment Script | Deployment script deployed configuration files without first backing up existing appliance configurations. | Added a timestamped backup directory and backup operations before configuration deployment. |

---

## 4. Testing & Verification Results

* **Date Tested:** [2026-11-25]
* **Target Environment:** [e.g., OSYS3030 Baseline Server (VMID 115)]
* **Verification Script Output:**
  ```text
  OSYS3030 Appliance Health & Verification Suite

BIND9 DNS Service........................PASS
Kea DHCPv4 Service.......................PASS
Host Hardening & SSH.....................PASS
Firewall & Routing.......................PASS

All appliance health checks passed successfully.
  ```

---

## 5. Attestation
I AI test that I have personally reviewed, tested, and understand every line of code in the generated scripts. I am prepared to explain any part of these scripts or configuration files during an evaluation.
