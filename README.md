# DISA STIG Windows 11 – Advanced Network Compliance Scan

## Project Overview

This project demonstrates a **Windows 11 compliance assessment** using the **DISA Microsoft Windows 11 STIG v2r5** within **Tenable Vulnerability Management**, deployed on a **Microsoft Azure Virtual Machine**.

The objective was to assess security configuration compliance, identify STIG violations, and document remediation strategies aligned with **security governance, risk management, and compliance (GRC)** principles.

---

## Objectives

- Perform an authenticated **STIG-based compliance scan**
- Identify Windows 11 security misconfigurations
- Analyze findings through a compliance and risk lens
- Propose remediation strategies aligned with DISA STIG guidance
- Demonstrate real-world compliance assessment workflows

---

## Environment & Architecture

- **Cloud Platform:** Microsoft Azure  
- **Target System:** Windows 11 Pro (x64) Virtual Machine  
- **Scan Platform:** Tenable Vulnerability Management  
- **Compliance Framework:** DISA Microsoft Windows 11 STIG v2r5  
- **Connectivity:** Azure Bastion (secure RDP)  
- **Network Security:** Azure Network Security Group (NSG)

<img src="images/VM.jpg" width="900">

<img src=images/VM2.jpg width="900">

<img src=images/VM3.jpg width="900">

---

## Secure VM Access (Azure Bastion)

Azure Bastion was used to securely access the Windows 11 VM without exposing it directly to the public internet, aligning with security best practices.

<img src="images/Bastion.jpg" width="900">

---

## Scan Configuration (Advanced Network Scan)

An **Advanced Network Scan** template was created in Tenable to support authenticated compliance auditing.

### Key Configuration Details
- Credentialed scan using a local Administrator account
- Remote Registry, Server service, and Admin Shares enabled
- Ping discovery and full TCP port scanning enabled
- Thorough assessment tests enabled
- DISA Microsoft Windows 11 STIG v2r5 added as a Compliance Audit

<img src="images/STIG.jpg" width="900">

---

## Findings Summary

The scan identified **132 total findings**, largely centered around configuration and policy enforcement gaps.

<img src="images/report.findings.jpg" width="900">

### Notable Findings
- Windows Defender Firewall disabled across all profiles
- Guest account enabled and assigned administrative privileges
- Weak password and account policy enforcement
- Outdated or vulnerable applications
- Untrusted or self-signed SSL certificates
- Excessive inbound network exposure via NSG rules

---

## Compliance Risk Analysis

These findings represent **direct violations of DISA STIG controls** and increase organizational risk by enabling:

- Privilege escalation through improper account management
- Network-based attacks due to weak firewall posture
- Credential compromise from insecure authentication policies
- Reduced audit readiness and regulatory compliance posture

---

## Solutions & Remediation Recommendations

### 1. Account & Privilege Management

**Issues Identified**
- Guest account enabled
- Guest account added to the Administrators group
- Insecure administrator account configuration

<img src=images/guestaccount.jpg width=600>

<img src="(https://github.com/briannameme17/DISA-STIG-Windows-11-Advanced-Network-Scan/blob/main/guestadministrators.jpg)" width="600">
### 2. Firewall & Network Security (NSG & Host-Based Firewall)

**Issues Identified**
- Azure Network Security Group (NSG) configured with overly permissive inbound rules (allow-all traffic)
- Windows Defender Firewall disabled across one or more profiles
- Increased exposure to unauthorized network access and lateral movement

**Recommended Solutions**
- Restrict NSG inbound rules to **only required ports and source IP ranges**
  - Remove any `Any → Any` allow rules
  - Implement a **deny-by-default** inbound rule set
- Limit management access (RDP/WinRM) to trusted IP addresses or private network access
- Enable **Windows Defender Firewall** for:
  - Domain Profile
  - Private Profile
  - Public Profile
- Ensure firewall rules align with **DISA STIG-approved configurations**
- Validate changes through a follow-up authenticated compliance scan

**Compliance Impact**
- Reduces attack surface and network exposure
- Aligns network and host-based controls with DISA STIG requirements
- Improves audit readiness and defense-in-depth posture

---

### 5. Continuous Compliance Monitoring

**Recommended Practices**
- Schedule recurring authenticated compliance scans
- Track STIG findings for trend and risk analysis
- Maintain remediation evidence for audits
- Align technical findings with governance and risk reporting

---

## Key Takeaways

This project demonstrates how **STIG-based compliance scanning supports governance and risk management objectives**. Mapping technical findings to compliance controls enables actionable insights for security, audit, and compliance stakeholders.

### Skills Demonstrated
- DISA STIG compliance assessment
- Vulnerability and configuration analysis
- Secure Azure VM deployment
- Risk-based remediation planning
- Governance, Risk, and Compliance (GRC) alignment

---

