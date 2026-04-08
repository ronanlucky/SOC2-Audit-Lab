# Audit Evidence — Exhibits A through F

This folder contains the six audit evidence exhibits supporting the control assessments in the SOC 2 Type I Audit Report. Each screenshot was captured from the live SOC Automation Lab environment during the audit period.

---

## Exhibit A — Windows Event Viewer: Event ID 4625

![Exhibit A](07-windows-event-viewer-4625.png)

**File:** `07-windows-event-viewer-4625.png`
**SOC 2 control:** CC6.7 — Logical Access Controls
**What it shows:** Windows Event Viewer on DESKTOP-8QQP7R4 filtered for Event ID 4625, showing 27 audit failure (failed logon) events logged between October 4–6, 2025. The event detail panel confirms EventID=4625, Keywords=Audit Failure, TaskCategory=Logon. This is the event source that feeds the entire detection pipeline.

---

## Exhibit B — Splunk Search: EventCode=4625 Detection

![Exhibit B](14-splunk-search-failed-logins.png)

**File:** `14-splunk-search-failed-logins.png`
**SOC 2 control:** CC7.2 — System Monitoring
**What it shows:** Splunk Enterprise (192.168.116.128) executing SPL query `index=soc_project EventCode=4625`, returning 5 events within the 24-hour window (10/9/25 to 10/10/25). Confirms the SIEM is ingesting Windows Security logs from the event source and correctly filtering on failed authentication indicators.

---

## Exhibit C — Splunk Alert Configuration: test-brute-force

![Exhibit C](15-splunk-alert-configuration.png)

**File:** `15-splunk-alert-configuration.png`
**SOC 2 control:** CC7.2 — Automated Alerting
**What it shows:** Splunk Searches, Reports, and Alerts panel showing the "test-brute-force" alert configured, enabled, and scheduled (next run: 2025-10-10 22:30:00 UTC). Alert type is confirmed as Alert, owner is soc_splunk, status shows ✓ Enabled. This demonstrates a documented, operational monitoring control.

---

## Exhibit D — n8n Workflow Executions: 5/5 Successful

![Exhibit D](25-n8n-execution-success.png)

**File:** `25-n8n-execution-success.png`
**SOC 2 control:** A1.2 — System Availability
**What it shows:** n8n workflow execution log (192.168.116.131:5678) showing 5 consecutive successful executions on October 6, 2025. Processing times range from 35ms to 8.954s. Workflow diagram confirms three-node pipeline: Webhook → OpenAI GPT-4 (Message a model) → Slack (Send a message). All executions completed without error.

---

## Exhibit E — Slack Alert Delivery: #alerts Channel

![Exhibit E](32-slack-alert-message.png)

**File:** `32-slack-alert-message.png`
**SOC 2 control:** CC7.3 — Incident Response Notification
**What it shows:** Slack #alerts channel (Soc_project workspace) showing an AI-generated security alert delivered on October 6th. Alert contains structured output with Event Type (Windows Security Event ID 4625), Timestamp, Computer (DESKTOP-8QQP7R4), User, Source IP (127.0.0.1), and Failed Attempts count. Confirms end-to-end notification delivery.

---

## Exhibit F — MITRE ATT&CK Mapping and Response Actions

![Exhibit F](33-slack-alert-details.png)

**File:** `33-slack-alert-details.png`
**SOC 2 control:** CC7.3 — AI-Enriched Threat Intelligence
**What it shows:** Continuation of the Slack alert showing GPT-4 enrichment output. Includes Severity Assessment (Low), MITRE ATT&CK Mapping (Tactic: Credential Access, Technique: Brute Force T1110), and Immediate Response Actions (verify user login attempt, check for repeated failures, ensure account is not locked). Demonstrates automated threat intelligence and structured incident response guidance.

---

## Evidence Chain

The six exhibits together cover the full detection pipeline end-to-end:

| Step | Exhibit | What it proves |
|---|---|---|
| 1 | A | Events are being generated and logged on the Windows source |
| 2 | B | Splunk is ingesting and querying those events |
| 3 | C | An automated alert rule is configured and active |
| 4 | D | The n8n automation pipeline executes reliably |
| 5 | E | Alerts are delivered to Slack successfully |
| 6 | F | GPT-4 enriches alerts with MITRE mapping and response actions |

---

*These exhibits are referenced in the [SOC2 Audit Report](../SOC2_Audit_Report.docx) and [SOC2 Audit Evidence Appendix](../SOC2_Audit_Evidence_Appendix.docx).*
