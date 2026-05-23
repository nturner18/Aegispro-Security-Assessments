# AegisPro CyberShield TX — Vulnerability Assessment Practice

> Documenting real-world security assessment engagements conducted by AegisPro CyberShield TX. This repository showcases the methodology, tooling, findings documentation, and remediation guidance produced during actual client engagements and ongoing practice assessments.

**Assessor:** Nick Turner, CISSP  
**Organization:** AegisPro CyberShield TX  
**Website:** [aegisprotx.com](https://www.aegisprotx.com)  
**Location:** Fort Worth, Texas

> **Confidentiality Notice:** All client engagements documented in this repository are anonymized to protect client identity and security posture. No identifying client information, IP addresses, credentials, or system-specific details are published. This repository is intended as a professional portfolio of methodology and process, not a disclosure of client vulnerabilities.

---

## Repository Structure

```
vulnerability-assessment-exercises/
├── README.md                          ← this file
├── engagements/
│   └── AEG-2026-001/                  ← Engagement ID: AEG-2026-001
│       ├── README.md                  ← full engagement write-up
│       ├── scope-and-roe.md           ← scope definition and rules of engagement
│       ├── methodology.md             ← assessment methodology followed
│       ├── findings.md                ← anonymized findings register
│       ├── remediation.md             ← remediation recommendations
│       └── screenshots/               ← sanitized scan output screenshots
├── methodology/
│   └── vulnerability-assessment-methodology.md   ← AegisPro standard methodology
└── templates/
    ├── assessment-template-full.md
    ├── assessment-template.md
    ├── checklist.md
    ├── intake-form-template-CGPT.md
    ├── intake-form-template-DS.md
    └── security_risk_assessment_intake.md
```

---

## Engagements

| Engagement ID | Client Type | Date | Scope | Findings | Status |
|--------------|------------|------|-------|----------|--------|
| [AEG-2026-001](./engagements/AEG-2026-001/README.md) | Property Preservation Services — DFW Area | April 2026 | Internal Network, Endpoint Security, Router/Firewall | 28 total (1H / 10M / 17L) | ✅ Complete |

---

## Methodology Overview

All AegisPro CyberShield TX vulnerability assessments follow a standardized six-phase lifecycle:

```
Phase 1 — Scoping & Authorization
└── Define engagement scope, obtain signed ROE, identify authorized systems

Phase 2 — Reconnaissance & Discovery
└── Host discovery, port scanning, service enumeration

Phase 3 — Vulnerability Scanning
└── Automated scanning via OpenVAS / GVM, Nmap, Nikto

Phase 4 — Analysis & Classification
└── Manual review of findings, false positive elimination, CVSS scoring

Phase 5 — Reporting
└── Preliminary findings summary, full technical report, remediation roadmap

Phase 6 — Remediation Guidance
└── Prioritized recommendations, follow-up consultation
```

Full methodology: [vulnerability-assessment-methodology.md](./methodology/vulnerability-assessment-methodology.md)

---

## Tools Used

| Tool | Purpose |
|------|---------|
| **OpenVAS / GVM** | Primary vulnerability scanner — unauthenticated and authenticated scans |
| **Nmap** | Host discovery, port scanning, service version detection |
| **Nikto** | Web server vulnerability scanning |
| **Kali Linux 2025.2** | Assessment platform |

---

## CISSP Domain Alignment

| Domain | Relevance |
|--------|-----------|
| Domain 1 — Security & Risk Management | Risk identification, vulnerability prioritization, engagement scoping |
| Domain 6 — Security Assessment & Testing | Vulnerability scanning methodology, findings analysis, reporting |
| Domain 7 — Security Operations | Tool operation, log analysis, detection awareness |

---

*AegisPro CyberShield TX | www.aegisprotx.com | nturner@aegisprotx.com*  
*Last updated: May 2026*
