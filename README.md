Web Application Security Assessment Report
Report Type: Surface-Level Security Audit
Target: (Not disclosed publically) with .com domain
Tester: Munnaza Jamil
Date: May 2026
Classification: Confidential — Portfolio Document

Executive Summary
A passive/Active and non-intrusive security assessment was conducted against the target web application. The assessment included DNS/WHOIS reconnaissance, port/service enumeration, and web server fingerprinting. Three findings were identified ranging from Informational to Medium severity.

Scope & Methodology
Assessment Type : Black-box, non-intrusive
Tools Used : Nmap, WPScan, WHOIS, Nikto 
Approach OWASP Testing Guide (OTG)
Authorization: Written permission obtained

Findings Summary:
NFS Service Exposed on Public Internet Medium Severity: Open
Web Application Firewall (WAF) Detected Informational: Noted
Web Server Version Finger printing Possible Low Severity: Open

Detailed Findings 
Finding 1 — NFS Service Exposed (Port 2049)
Severity: 🟡 Medium
Description:
Network File System (NFS) service was found running and accessible on port 2049/tcp from the public internet. 
NFS is a file-sharing protocol designed for internal/private network use only.

Evidence:
PORT: 2049/tcp
STATE: open
SERVICE VERSION: nfs     3-4 (RPC #100003)
   
Risk:
If NFS exports are misconfigured, an unauthenticated attacker could potentially read or write files on the server. This also increases the attack surface unnecessarily.

Recommendation:
Block port 2049 at the firewall for all external traffic
Restrict NFS access to trusted internal IPs only
If NFS is not required, disable the service entirely


Finding 2 — WAF Presence Detected
Severity: ℹ️ Informational
Description:
A Web Application Firewall (WAF) was detected during scanning, returning HTTP 403 responses to automated scanner traffic. This is a positive security control.
Evidence:
WPScan result: "The target is responding with a 403, 
this might be due to a WAF"
Recommendation:
WAF is good practice. Ensure it is regularly updated and rules are tuned to prevent bypass techniques.

Finding 3 — Web Server Version Disclosure
Severity: 🔵 Low
Description:
The web server identified itself as OpenResty through service banner responses. Exposing server technology allows attackers to research version-specific vulnerabilities.
Evidence:
80/tcp  open  http     OpenResty web app server
443/tcp open  ssl/http OpenResty web app server

Recommendation:
Suppress server version banners in HTTP response headers

Positive Security Observations:
HTTPS (port 443) is active — encrypted traffic in use ✅
WAF is deployed ✅
No critical open ports beyond expected services ✅


Disclaimer
This assessment was conducted with explicit written authorization from the target owner. Findings reflect a point-in-time assessment and may not represent all vulnerabilities present. This report is for portfolio/sample purposes with all identifying information redacted.
