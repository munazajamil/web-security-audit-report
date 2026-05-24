# 🛡️ Web Application Security Assessment Report

> **Portfolio Sample** — Target URL and identifying details have been redacted. This report demonstrates real methodology applied during a surface-level black-box audit conducted with written client authorization.

---

## 📋 Report Overview

| Field | Details |
|-------|---------|
| **Report Type** | Surface-Level Web Security Audit |
| **Target** | Confidential `.com` domain *(not disclosed publicly)* |
| **Tester** | Munnaza Jamil |
| **Date** | May 2026 |
| **Classification** | Confidential — Portfolio Document |
| **Authorization** | Written permission obtained from target owner |

---

## 🔍 Executive Summary

A **passive and active, non-intrusive** security assessment was conducted against the target web application. The engagement included:

- 🔎 DNS & WHOIS reconnaissance
- 🌐 Port and service enumeration
- 🖥️ Web server fingerprinting
- 🔧 Automated vulnerability scanning

**3 findings** were identified across the assessment, ranging from **Informational** to **Medium** severity. No critical vulnerabilities were discovered. One positive security control (WAF) was confirmed active.

---

## 🧪 Scope & Methodology

### Assessment Parameters

| Parameter | Detail |
|-----------|--------|
| **Assessment Type** | Black-box, non-intrusive |
| **Tools Used** | `Nmap` `WPScan` `WHOIS` `Nikto` |
| **Framework** | OWASP Testing Guide (OTG) |
| **Authorization** | ✅ Written permission obtained |
| **Scan Depth** | Surface-level — no exploitation attempted |

### Tools Used

| Tool | Purpose |
|------|---------|
| `Nmap -sV` | Port scanning & service version detection |
| `WPScan` | WordPress vulnerability & plugin enumeration |
| `Nikto` | Web server misconfiguration scanning |
| `WHOIS` | Domain registration & ownership lookup |

---

## 📊 Findings Summary

| # | Finding | Severity | Status |
|---|---------|----------|--------|
| 1 | NFS Service Exposed on Public Internet | 🟡 **Medium** | 🔴 Open |
| 2 | WAF (Web Application Firewall) Detected | ℹ️ **Informational** | ✅ Noted |
| 3 | Web Server Version Fingerprinting Possible | 🔵 **Low** | 🟠 Open |

---

## 🔎 Detailed Findings

---

### Finding 1 — NFS Service Exposed on Public Internet

| Field | Detail |
|-------|--------|
| **Severity** | 🟡 Medium |
| **Port** | 2049/tcp |
| **Status** | Open |
| **CVSS Category** | Network Misconfiguration |

#### Description

Network File System (NFS) service was found **running and accessible on port 2049/tcp from the public internet**. NFS is a file-sharing protocol designed strictly for internal/private network use. Its exposure on a public-facing server is a significant misconfiguration.

#### Evidence

```
PORT      STATE   SERVICE   VERSION
2049/tcp  open    nfs       3-4 (RPC #100003)
```

#### Risk

> If NFS exports are misconfigured, an **unauthenticated remote attacker** could potentially:
> - Read sensitive files from server exports
> - Write or modify files on mounted shares
> - Leverage access for further lateral movement

This finding also unnecessarily increases the server's **external attack surface**.

#### Recommendations

- [ ] Block port `2049` at the firewall for **all external/inbound traffic**
- [ ] Restrict NFS access to **trusted internal IPs only** via `/etc/exports`
- [ ] If NFS is not actively required, **disable the service entirely**
- [ ] Audit current NFS exports using `showmount -e <host>` from an internal network

---

### Finding 2 — WAF (Web Application Firewall) Detected

| Field | Detail |
|-------|--------|
| **Severity** | ℹ️ Informational |
| **Status** | Noted — Positive Control |

#### Description

A **Web Application Firewall (WAF)** was detected during scanning. The target returned **HTTP 403 Forbidden** responses to automated scanner traffic, indicating active WAF filtering. This is a **positive security control**.

#### Evidence

```
WPScan Output:
"Scan Aborted: The target is responding with a 403,
this might be due to a WAF."
```

#### Recommendations

- [ ] Ensure WAF rulesets are **regularly updated**
- [ ] Tune rules to defend against **WAF bypass techniques** (encoding, header manipulation)
- [ ] Periodically test WAF effectiveness using controlled assessments

---

### Finding 3 — Web Server Version Fingerprinting Possible

| Field | Detail |
|-------|--------|
| **Severity** | 🔵 Low |
| **Port** | 80/tcp, 443/tcp |
| **Status** | Open |

#### Description

The web server **identified itself as OpenResty** through service banner responses during port scanning. Exposing server technology and version information allows attackers to **research known CVEs** specific to that version and craft targeted attacks.

#### Evidence

```
PORT    STATE  SERVICE   VERSION
80/tcp  open   http      OpenResty web app server
443/tcp open   ssl/http  OpenResty web app server
```

#### Recommendations

- [ ] Suppress server version banners in HTTP response headers
- [ ] Add the following to OpenResty/Nginx configuration:
  ```nginx
  server_tokens off;
  ```
- [ ] Remove or customize the `Server:` HTTP response header
- [ ] Consider using a reverse proxy to further mask backend technology

---

## ✅ Positive Security Observations

The following security controls were **confirmed active** during assessment:

| Control | Status |
|---------|--------|
| 🔒 HTTPS (Port 443) active — encrypted traffic in use | ✅ Present |
| 🛡️ Web Application Firewall (WAF) deployed | ✅ Present |
| 🚫 No critical ports exposed beyond expected web services | ✅ Confirmed |

---

## 📸 Evidence Screenshots

> *Screenshots of scan outputs are included below. All identifying information (URLs, IPs) has been blurred for client confidentiality.*

| Screenshot | Description |
|------------|-------------|
| `nmap_scan.png` | Nmap service version scan output |
| `whois_lookup.png` | WHOIS domain reconnaissance result |

---

## 📁 Repository Structure

```
web-security-audit-sample/
├── README.md               ← This report
├── screenshots/
│   ├── nmap_scan.png       ← Blurred Nmap output
│   └── whois_lookup.png    ← Blurred WHOIS output
```

---

## ⚠️ Disclaimer

> This assessment was conducted with **explicit written authorization** from the target owner.
> Findings reflect a **point-in-time assessment** and may not represent all vulnerabilities present.
> This report is published for **portfolio and educational purposes only**, with all identifying information redacted.
> Unauthorized scanning or testing of systems without permission is **illegal** and unethical.

---

## 👩‍💻 About the Tester

**Munnaza Jamil** — SOC Analyst & Cybersecurity Researcher

- 🔗 [GitHub](https://github.com/munazajamil)
- 🔗 [LinkedIn](https://linkedin.com/in/munazajamil/)
- 🌐 [Blog](https://munazajameel.site/blog)
- 🎓 Cybersecurity Diploma — PNY Rawalpindi
- 🧪 TryHackMe | Wazuh SIEM | MITRE ATT&CK | OSINT

---

*Report generated using OWASP OTG methodology | May 2026*
