# Engagement AEG-2026-001
## Internal Network Security Assessment
### AegisPro CyberShield TX

---

> **Confidentiality Notice:** This engagement write-up is anonymized. The client name, contact details, specific IP addresses, and system-specific identifiers have been removed or generalized to protect client confidentiality. This document is published as a demonstration of AegisPro CyberShield TX's assessment methodology and professional practice.

---

## Engagement Overview

| Field | Details |
|-------|---------|
| Engagement ID | AEG-2026-001 |
| Client Type | Property Preservation Services — DFW Area, Texas |
| Business Profile | Small business, 3 employees, 1 location, no dedicated IT staff |
| Lead Assessor | Nicholas Turner, CISSP |
| Assessment Date | April 9, 2026 |
| Testing Window | 12:00 PM – 4:00 PM (4 hours) |
| Assessment Type | Internal Network Vulnerability Assessment |
| Delivery Method | On-site |

---

## Scope

### Areas Assessed

| Area | Included |
|------|----------|
| Internal Network Scan | ✅ Yes |
| Endpoint Security Review | ✅ Yes |
| Router / Firewall Review | ✅ Yes |
| External Network Scan | ❌ No |
| Web Application Review | ❌ No |
| POS System Review | ❌ No |
| Cloud Environment Review | ❌ No |
| Compliance Gap Review | ❌ No |

### Authorized Activities

| Activity | Authorized |
|----------|-----------|
| Network vulnerability scanning | ✅ Yes |
| Port and service enumeration | ✅ Yes |
| Security configuration review | ✅ Yes |
| Wireless network review | ✅ Yes |
| Endpoint security checks | ✅ Yes |
| Firewall exposure testing | ❌ No |
| Credential testing | ❌ No |
| Denial-of-Service testing | ❌ No |
| Social engineering | ❌ No |
| Data exfiltration simulation | ❌ No |

### Network Range

Internal network segment: `192.168.1.0/24`

### Scan Type

**Unauthenticated** — No credentials were provided to the scanner. All findings represent vulnerabilities detectable by an attacker with only network access, without privileged system access.

---

## Client Environment Profile

| Component | Details |
|-----------|---------|
| Internet Provider | Charter Spectrum |
| Number of Endpoints | Small footprint — residential-grade infrastructure |
| Cybersecurity Insurance | None |
| Designated IT Staff | None |
| Regulatory Requirements | None identified |

**Intake observations:** The client had no dedicated IT or security resources, no cybersecurity insurance, and no documented security policies in place prior to this engagement. This is a common profile for small businesses in the DFW area and represents the core target market for AegisPro CyberShield TX's services.

---

## Methodology

### Phase 1 — Scoping & Authorization

Prior to any testing activity:

1. Completed intake form documenting client business profile, IT infrastructure, and assessment scope
2. Executed a signed Rules of Engagement (ROE) and Authorization document via Dropbox Sign
3. ROE defined: authorized scope, testing window, prohibited actions, confidentiality obligations, and liability terms
4. Client confirmed as authorized representative (Co-Owner/Supervisor)
5. Authorization was obtained and confirmed before a single scan was run

> **Why this matters:** A signed authorization document is not optional — it is a legal and ethical requirement for any security assessment. The ROE protects both the assessor and the client, defines the boundaries of the engagement, and establishes accountability. AegisPro CyberShield TX requires signed authorization for every engagement before any technical work begins.

### Phase 2 — Host Discovery

Network discovery was performed to identify all live hosts on the authorized `192.168.1.0/24` range:

```bash
nmap -sn 192.168.1.0/24
```

This returned a list of all active devices on the network, which were then enumerated further in Phase 3.

### Phase 3 — Port & Service Enumeration

Each discovered host was enumerated for open ports, running services, and service versions:

```bash
nmap -sV -sC -O <target-IP> -oN nmap-results.txt
```

Service version information was captured to provide context for vulnerability scanner findings and to identify potentially dangerous or unexpected services running on internal devices.

### Phase 4 — Vulnerability Scanning

**Tool:** OpenVAS / GVM (Greenbone Vulnerability Manager)  
**Scan type:** Unauthenticated  
**Scan configuration:** Full and Fast

The OpenVAS scan was executed against all discovered hosts within the authorized range. Scan results were reviewed in their entirety before findings were classified, with manual review performed to identify and eliminate false positives.

```
Scan configuration: Full and Fast
Scan type: Unauthenticated
Target: 192.168.1.0/24
Duration: Completed within the 12:00 PM – 4:00 PM testing window
```

![OpenVAS scan in progress](./screenshots/openvas-scan.png)

### Phase 5 — Findings Analysis & Classification

Each finding returned by OpenVAS was reviewed manually and classified using the AegisPro CVSS-based severity framework:

| Severity | CVSS Range | Remediation Timeline |
|----------|-----------|---------------------|
| Critical | 9.0–10.0 | Immediate — within 24 hours |
| High | 7.0–8.9 | Urgent — within 7 days |
| Medium | 4.0–6.9 | Standard — within 30 days |
| Low | 0.1–3.9 | Routine — next maintenance cycle |
| Informational | N/A | No required timeline |

False positives were identified and removed before the final count was recorded.

### Phase 6 — Reporting & Delivery

Two deliverables were produced and delivered to the client:

1. **Preliminary Findings Summary** — Signed and delivered on the day of assessment; covers risk overview, example findings, risk statement, and immediate recommendations
2. **Full Security Risk Assessment Report** — Complete technical findings, device-by-device analysis, remediation roadmap, and executive summary

---

## Findings Summary

| Severity | Count |
|----------|-------|
| **Critical** | 0 |
| **High** | 1 |
| **Medium** | 10 |
| **Low** | 17 |
| **Informational** | 0 |
| **Total** | **28** |

![OpenVAS report findings summary](./screenshots/findings-summary.png)

---

## Notable Findings

### High Severity

**Weak VNC Authentication Detected on Internal Device**

A VNC (Virtual Network Computing) service was identified on an internal device that was configured to allow login using weak or default authentication. VNC provides full graphical remote access to the target system — weak authentication on this service means any attacker with network access could gain complete control of the affected device without requiring valid credentials.

**Why this matters for a small business:** An attacker who gains VNC access to an internal machine has the same access as a person sitting at that keyboard — they can access files, install software, modify configurations, and use the machine as a pivot point to attack other devices on the network.

**Remediation:** Disable VNC if remote access is not required. If required, implement strong password authentication, restrict access to specific IP addresses, and place the service behind a VPN.

---

### Representative Medium Findings

**Cleartext Transmission of Credentials over HTTP**

Certain internal web interfaces were identified transmitting authentication credentials over unencrypted HTTP rather than HTTPS. This means credentials submitted through these interfaces travel across the network in plaintext — any device on the same network segment capable of capturing traffic can read them directly.

**Why this matters:** In a small office environment where multiple devices share the same network, credential exposure via HTTP is a realistic and exploitable risk.

**Remediation:** Enforce HTTPS with a valid TLS certificate on all web interfaces that require authentication. Redirect HTTP to HTTPS at the server level.

---

## Risk Statement

The preliminary assessment identified that several internal systems are configured with outdated encryption protocols, weak authentication mechanisms, and insecure network services. While no critical vulnerabilities were identified, the presence of high and medium severity issues indicates that the organization could be exposed to internal network compromise, credential interception, or unauthorized access if these weaknesses remain unaddressed.

---

## Recommendations

The following actions were recommended to the client in priority order:

1. **Immediately** — Replace weak or default credentials on all remote access services (VNC, RDP, any management interfaces)
2. **Within 30 days** — Enforce encrypted communications (HTTPS / TLS) on all internal web interfaces requiring authentication
3. **Within 30 days** — Review and update all network devices (router, firewall, access points) to current firmware versions
4. **Ongoing** — Establish a basic patch management process — at minimum, enable automatic updates on all endpoints
5. **Recommended** — Obtain cybersecurity insurance — given the absence of any current policy, the client has no financial protection in the event of a breach
6. **Recommended** — Engage AegisPro CyberShield TX for an ongoing managed security services engagement to maintain security posture over time

---

## Lessons Learned / Assessor Notes

> *These notes are internal observations documented for professional development purposes.*

- Unauthenticated scanning of a small residential-grade network produces a high proportion of Low findings related to firmware age and default configurations — this is typical for small business environments without dedicated IT
- The absence of any IT staff or security resource meant there was no baseline security posture to compare against — the assessment served as a true first-look at the environment
- The VNC finding was the most significant risk in the environment — it represented a clear path to full system compromise for any attacker with internal network access
- Cleartext credential transmission findings are consistently underestimated by small business clients — the "no one would want to hack us" mindset is common and represents an education opportunity
- A 4-hour testing window was sufficient for a small residential-grade network — larger environments would require significantly more time

---

## CISSP Domain Alignment

| Domain | Activities in this Engagement |
|--------|------------------------------|
| Domain 1 — Security & Risk Management | Client risk identification, engagement scoping, ROE execution |
| Domain 6 — Security Assessment & Testing | Vulnerability scanning methodology, findings analysis, severity classification, reporting |
| Domain 7 — Security Operations | Tool operation, scan analysis, detection awareness |

---

## Documents

| Document | Description | Status |
|----------|-------------|--------|
| Intake Form | Client business profile and infrastructure overview | ✅ On file |
| Rules of Engagement / Authorization | Signed authorization for testing — Dropbox Sign audit trail | ✅ Signed |
| Preliminary Findings Summary | Same-day delivery to client | ✅ Delivered |
| Full Security Risk Assessment Report | Complete technical findings and remediation roadmap | ✅ Delivered |

---

*AegisPro CyberShield TX | Engagement AEG-2026-001 | April 2026*  
*Lead Assessor: Nicholas Turner, CISSP*
