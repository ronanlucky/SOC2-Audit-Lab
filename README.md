# SOC 2 Type I Audit — SOC Automation Lab

A end-to-end simulated SOC 2 Type I audit conducted against a personal SOC Automation Lab. This project demonstrates practical GRC and audit methodology including risk assessment, control mapping, and formal findings documentation — applied to a real, working security pipeline.

---

## Project Overview

| Detail | Value |
|---|---|
| Audit subject | [SOC Automation Lab](https://github.com/ronanlucky/SOC-Automation-Lab) |
| Audit type | SOC 2 Type I (point-in-time, control design) |
| Trust Service Criteria | Security (CC6, CC7) · Availability (A1) |
| Methodology | NIST SP 800-30 Rev. 1 · AICPA SOC 2 TSC 2017 |
| Audit date | April 7, 2026 |
| Author | Ronan Kongala — MS Cybersecurity, Northeastern University |

---

## System Under Audit

The SOC Automation Lab is a fully functional security operations pipeline built with:

| Component | Technology | Role |
|---|---|---|
| Event source | Windows 10 + Sysmon | Generates Event ID 4625 (failed logon) |
| SIEM | Splunk Enterprise | Log aggregation, SPL queries, alerting |
| Orchestration | n8n (Docker) | Webhook → GPT-4 → Slack automation |
| AI analysis | OpenAI GPT-4 | Threat enrichment, MITRE ATT&CK mapping |
| Notification | Slack | Alert delivery to #alerts channel |

---

## Audit Phases

### Phase 1 — Scope & Planning
Defined the system boundary, selected Trust Service Criteria (Security + Availability), documented in-scope components, and established the audit date.

📄 [SOC2_Audit_Scope_Document.docx](https://github.com/ronanlucky/SOC2-Audit-Lab/blob/main/SOC2_Audit_Scope_Document.docx)



---

### Phase 2 — Risk Register
Identified and rated 10 risks across the full pipeline using NIST SP 800-30 Rev. 1. Each risk is assessed by likelihood, impact, and risk score, with a recommended control and current status.

| Risk ID | Component | Threat | Rating |
|---|---|---|---|
| R-01 | Splunk SIEM | Brute force on Splunk admin account | High |
| R-02 | n8n | Unauthenticated webhook endpoint | Medium |
| R-03 | OpenAI API | API key exposure via logs | Medium |
| R-04 | Windows VM | Lateral movement between VMs | Medium |
| R-05 | Splunk SIEM | Disk space exhaustion causing outage | Medium |
| R-06 | n8n | Docker container crash, no restart policy | Medium |
| R-07 | Slack | Slack bot token compromise | Medium |
| R-08 | Windows VM | Alert flooding from single-event threshold | Medium |
| R-09 | Network | VM IP change breaks automation pipeline | Medium |
| R-10 | OpenAI API | AI prompt injection via malicious log data | Medium |

📄 [SOC2_Risk_Register.docx](https://github.com/ronanlucky/SOC2-Audit-Lab/blob/main/SOC2_Risk_Register.docx)

---

### Phase 3 — Control Mapping Matrix
Mapped 14 controls across CC6 (Logical Access), CC7 (System Operations), and A1 (Availability) to the SOC 2 Trust Service Criteria. Each control is assessed for implementation status and gaps.

| Status | Count |
|---|---|
| Implemented | 4 |
| Partially implemented | 9 |
| Not implemented | 0 |

📄 [SOC2_Control_Matrix.docx](https://github.com/ronanlucky/SOC2-Audit-Lab/blob/main/SOC2_Control_Matrix.docx)

---

### Phase 4 — Audit Report
Formal SOC 2 Type I audit report with auditor opinion, system description, performance baseline, 6 detailed findings, and a prioritized remediation roadmap.

**Finding summary:**

| ID | Finding | TSC | Severity |
|---|---|---|---|
| F-01 | Splunk web interface operates over unencrypted HTTP | CC6.1 | High |
| F-02 | n8n webhook endpoint accepts unauthenticated requests | CC6.6 | Medium |
| F-03 | API keys stored without secrets management or rotation policy | CC6.7 | Medium |
| F-04 | Alert rule triggers on single failed logon with no threshold | CC7.2 | Medium |
| F-05 | n8n Docker container has no restart policy configured | A1.2 | Medium |
| F-06 | Splunk disk space threshold set below recommended minimum | A1.2 | Medium |

📄 [SOC2_Audit_Report.docx](https://github.com/ronanlucky/SOC2-Audit-Lab/blob/main/SOC2_Audit_Report.docx)

---

### Evidence Appendix
Six labeled audit exhibits captured from the live SOC lab environment, embedded in a formal evidence document with audit-language descriptions and TSC references.

| Exhibit | Screenshot | Control supported |
|---|---|---|
| A | Windows Event Viewer — 27 Event ID 4625 failures | CC6.7 |
| B | Splunk search — EventCode=4625 detection | CC7.2 |
| C | Splunk alert configuration — test-brute-force | CC7.2 |
| D | n8n execution log — 5/5 successful runs | A1.2 |
| E | Slack alert delivery — #alerts channel | CC7.3 |
| F | MITRE ATT&CK mapping — T1110 Brute Force | CC7.3 |

📄 [SOC2_Audit_Evidence_Appendix.docx](https://github.com/ronanlucky/SOC2-Audit-Lab/blob/main/SOC2_Audit_Evidence_Appendix.docx)

---

## Key Results

- **14 controls** mapped across Security and Availability criteria
- **10 risks** assessed using NIST SP 800-30 likelihood-impact scoring
- **6 findings** documented with Condition / Criteria / Cause / Effect / Recommendation
- **100% detection rate** confirmed for Event ID 4625 across the pipeline
- **< 60 second** event-to-alert time validated end-to-end

---

## Skills Demonstrated

- SOC 2 Trust Service Criteria (Security, Availability)
- NIST SP 800-30 risk assessment methodology
- Control design assessment and gap analysis
- Audit evidence collection and documentation
- Formal findings writing (Condition / Criteria / Cause / Effect)
- MITRE ATT&CK framework mapping
- GRC tooling concepts (control registers, risk registers, audit workpapers)

---

## Related Project

This audit was conducted against the [SOC Automation Lab](https://github.com/ronanlucky/SOC-Automation-Lab) — an automated SOC pipeline using Splunk, n8n, OpenAI GPT-4, and Slack.

---

## Contact

**Ronan Kongala**
MS Cybersecurity · Northeastern University
[linkedin.com/in/ronan-kongala](https://linkedin.com/in/ronan-kongala-99068a240/)
ronanlucky@gmail.com

---

> *This project is a simulated audit conducted for portfolio and learning purposes. It does not constitute a formal AICPA-accredited SOC 2 examination.*
