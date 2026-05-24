Skip to content
munazajamil
web-security-audit-report
Repository navigation
Code
Issues
Pull requests
Actions
Projects
Wiki
Security and quality
Insights
Settings
Files
Go to file
t
T
screenshots
README.md
web-security-audit-report
/
README.md
in
main

Edit

Preview
Indent mode

Spaces
Indent size

2
Line wrap mode

Soft wrap
Editing README.md file contents
Selection deleted
  1
  2
  3
  4
  5
  6
  7
  8
  9
 10
 11
 12
 13
 14
 15
 16
 17
 18
 19
 20
 21
 22
 23
 24
 25
 26
 27
 28
 29
 30
 31
 32
 33
 34
 35
 36
 37
 38
 39
 40
 41
 42
 43
 44
 45
 46
 47
 48
 49
 50
 51
 52
 53
 54
 55
 56
 57
 58
 59
 60
 61
 62
 63
 64
 65
 66
 67
 68
 69
 70
 71
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
Use Control + Shift + m to toggle the tab key moving focus. Alternatively, use esc then tab to move to the next interactive element on the page.
No file chosen
Attach files by dragging & dropping, selecting or pasting them.
