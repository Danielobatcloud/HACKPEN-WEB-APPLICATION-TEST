# HACKPEN-WEB-APPLICATION-TEST
Penetration Testing Report

Penetration Test for 10.129.32.179
Test Execution: Kalilinux, Penligent

I. Executive Summary

1.1 Confidentiality Statement

This document is the exclusive property of Hacpen Consulting and contains proprietary and confidential information. Any reproduction, distribution, or use (in whole or in part) requires written permission from Hacpen Consulting.

1.2 Report Overview

2026-05-29, Daniel Obatuyise(CITP) conducted a web application penetration test on 10.129.32.179 to assess its security posture and identify potential attack risks. The core purpose of this penetration test is to proactively discover vulnerabilities in the target system/application/asset.
This assessment aims to simulate a real attacker to identify cybersecurity risks that may affect the confidentiality of sensitive data and the integrity of information systems. The scope is limited to production web applications hosted within 10.129.32.179 (IP/domain).

1.3 Testing Authorization Statement

This penetration testing activity has been formally authorized by the target system owner.
All testing activities were conducted within the mutually confirmed scope of authorization, focusing solely on approved assets for security assessment.

Testing strictly adhered to established testing rules to avoid business interruption or data corruption to production systems.

1.4 Vulnerability Distribution

Severity      Count
Critical        0
High            1
Medium          1
Low             0
Informational   0

1.5 Overall Risk Assessment and Conclusion
Moderate risk with high vulnerabilities that should be addressed promptly.

II. Engagement Overview

2.1 Objectives

The objectives of this penetration test are:
. Identify security vulnerabilities
. Assess attack surface exposure
. Evaluate the effectiveness of security controls
. Provide remediation and improvement recommendations

2.2 Engagement Type

. External penetration testing
. Web application security testing
. Vulnerability assessment

2.3 Test Type

This penetration test employed an external Black Box testing approach.
Testers conducted security assessments from an attacker's perspective without access to internal system information.

III. Test Scope

The scope of this penetration test included the following assets:

3.1 Target Basic Information

. Target: 10.129.32.179
. Target Type: IP

3.2 Out of Scope:

The following items were not within the scope of this test:

. Social engineering attacks
. Physical security testing
. Denial of Service (DoS) attacks

IV. Testing Rules

The following rules were confirmed by both parties before testing:

. Testing was conducted only on authorized assets
. System service interruptions were avoided during testing
. Vulnerability exploitation was limited to proof-of-concept (PoC)
. No extraction or leakage of sensitive production data
. All testing activities were conducted within the agreed time window

V. Testing Methodology

The penetration testing process included the following phases:

Phase 1: Reconnaissance and Asset Enumeration (P1)

. P1: Full Port and Service Discovery
. P1: Web Path and Sensitive File Enumeration
. P1: DNS and Virtual Host Enumeration
. P0: Analyze and Test Exposed FTP Credentials
. P0: Analyze and Test Exposed FTP Credentials
. P0: Analyze and Test Exposed FTP Credentials
. P0: Analyze and Test Exposed FTP Credentials
. P0: Analyze and Test Exposed FTP Credentials
. P0: Analyze and Test Exposed FTP Credentials

Phase 2: Service Identification and Technical Fingerprinting (P1)

. P1: Web Technology Stack Fingerprinting
. P1: SSL/TLS Configuration and Vulnerability Analysis

Phase 3: High-Risk Vulnerability Verification (P0)

. P0: Remote Code Execution and Command Injection Detection
. P0: Input Point Injection Vulnerability Detection
. P0: Sensitive Configuration and File Exposure Detection

Phase 4: Common Web and API Vulnerability Detection (P1)

. P1: Cross-Site Scripting and Client-Side Injection Detection
. P1: Server-Side Request Forgery (SSRF) Detection
. P1: File Upload and Unrestricted Resource Consumption Testing

Phase 5: Authentication Authorization and Business Logic Testing (P2)

. P2: Default Credentials and Weak Authentication Testing
. P2: IDOR and Access Control Verification
. P2: Business Logic and Workflow Abuse Testing

5.1 Testing Standards

This penetration test referenced the following industry security testing standards:

. NIST SP 800-115 (Technical Guide to Information Security Testing and Assessment)
. OWASP Testing Guide (Web Application Security Testing Guide)
. OWASP Top 10 (Top 10 Web Application Security Risks)
. PTES (Penetration Testing Execution Standard)
. These standards were used to guide the testing process, vulnerability identification methods, and report writing             specifications for this penetration test.

VI. Attack Surface Overview

The attack surface exposed by the system includes:

. Public-facing web applications
. API interfaces
. Server infrastructure
. Authentication mechanisms
. Third-party dependency components

VII. Risk Rating Methodology

Vulnerability risk levels are assessed based on CVSS standards.

. Critical: CVSS score ≥9.0
. High: 7.0≤CVSS<9.0
. Medium: 4.0≤CVSS<7.0
. Low: CVSS<4.0
. Informational: CVSS score unknown or no impact

Risk assessment considers the following factors:

. Difficulty of vulnerability exploitation
. Impact scope of attack
. System exposure level

VIII. Tools and Technologies Used

The following tools and technologies were used in this penetration test:

Kali Linux
Penligent: Autonomous AI Hacker
sqlmap: SQL injection testing
whatweb: Web fingerprinting
nmap: Port scanning
Python requests: Batch testing

Manual security testing was also performed when automated tools could not identify issues.

IX. Vulnerability Summary

No. F-001
Title: Credential Files Exposed via Anonymous FTP                  
Target: 10.129.32.179:21 - allowed.userlist / allowed.userlist.passwd                
Severity: High                    
Status: Not Remediated


No. F-002
Title: Anonymous FTP Login Enabled
Target Version: 10.129.32.179:21 (vsftpd 3.0.3)
Severity: Medium
Status: Not Remediated

X. Detailed Findings

Risk ID F-1: Credential Files Exposed via Anonymous FTP

. Risk Level: high
. CVSS Score: 7.5
. Affected System: 10.129.32.179:21 - allowed.userlist / allowed.userlist.passwd
. Vulnerability Description: The files 'allowed.userlist' (418 bytes) and 'allowed.userlist.passwd' (1778 bytes) are           accessible to anonymous FTP users. The file names strongly suggest they contain usernames and corresponding passwords for    system or application access. These credentials could be used to gain unauthorized access to other services (SSH, web        admin panels, etc.) on the target host.

Remediation Recommendation: Immediately remove or relocate credential files from the FTP directory. Disable anonymous FTP access. Audit all services for credential reuse using the exposed passwords.

Evidence:
ftp anonymous login + LIST (Round 1)
. Evidence: Anonymous login successful. Files: allowed.userlist (418 B), allowed.userlist.passwd (1778 B), dated Feb 25 2021.

ftp RETR (Round 2)
. Evidence: Both files successfully downloaded via anonymous FTP; non-zero sizes confirm substantive content.

Risk ID F-2: Anonymous FTP Login Enabled

. Risk Level: medium
. CVSS Score: 5.3
. Affected System: 10.129.32.179:21 (vsftpd 3.0.3)
. Vulnerability Description: The vsftpd 3.0.3 FTP server on port 21 permits anonymous login without any authentication. This   allows unauthenticated users to browse the FTP directory, enumerate files, and download potentially sensitive content. The   directory listing revealed files named 'allowed.userlist' and 'allowed.userlist.passwd' that are world-readable to           anonymous users.

. Remediation Recommendation: Disable anonymous FTP login by setting 'anonymous_enable=NO' in /etc/vsftpd.conf. If anonymous   access is required for business reasons, restrict it to a chrooted jail with no sensitive files and enforce read-only        access.

Evidence:

. tool_id:41 (ftp anonymous login)
 
  Evidence:
  230 Login successful.
  Remote system type is UNIX.
  Using binary mode to transfer files.
  -rw-r--r--    1 0        0             418 Feb 25  2021 allowed.userlist
  -rw-r--r--    1 0        0            1778 Feb 25  2021 allowed.userlist.passwd

XI. Remediation Recommendations

High Findings:

. Address high severity vulnerabilities promptly.
. Enforce strong password policies and consider implementing multi-factor authentication (MFA).
. Review and strengthen authentication and authorization mechanisms.

Medium Findings:

. Review and remediate medium severity issues in a timely manner.
. Review HTTP headers to ensure sensitive data is not exposed.
. Update security configurations and settings.

11.1 Vulnerability Remediation Priority

It is recommended to establish the following remediation timeframes based on vulnerability severity:
. Critical: Remediate within 1 week
. High: Remediate within 30 days
. Medium: Remediate within 60-90 days
. Low: Schedule remediation based on business circumstances

11.2 Vulnerability Retesting

After vulnerability remediation is complete, retesting is recommended to verify that vulnerabilities have been successfully fixed.

The purposes of retesting include:

. Verify the effectiveness of vulnerability remediation
. Confirm that no new security issues have been introduced to the system
. Update vulnerability status (Fixed / Not Fixed / Risk Accepted)
. Retest results should be documented and preserved as part of the security management system.

XII. Compliance Statement

This penetration test can support the following security compliance requirements:

SOC 2
. Security controls
. Monitoring mechanisms
. Vulnerability management

ISO 27001
. A.12.6 Technical vulnerability management
. A.14.2 Security in system engineering
. A.18 Compliance review

XIII. Testing Limitations

This security assessment is a point-in-time test conducted within a specific time window.
New security risks may emerge as system configurations change, new features are launched, or new attack techniques appear.

Therefore, it is recommended that organizations conduct regular security testing and vulnerability scanning to continuously improve overall security protection capabilities.

XIV. Conclusion

In conclusion, the penetration test identified several critical and/or high vulnerabilities that require immediate remediation. The organization should address these vulnerabilities as a priority to mitigate the risk of unauthorized access and potential data breaches. Once the vulnerabilities are remediated, a retest should be conducted to verify the effectiveness of the fixes.

Prepared by: Daniel Obatuyise
Date: 2026-05-29

