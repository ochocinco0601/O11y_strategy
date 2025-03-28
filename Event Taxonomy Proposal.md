# Event Taxonomy Proposal

## 1. Purpose
This document proposes a standardized taxonomy for classifying events across observability, monitoring, alerting, and incident response systems. A shared classification system improves:

- Consistency in triage and response
- Quality of alert routing and prioritization
- Correlation between system behavior and business impact
- Incident reporting, analytics, and executive communication

---

## 2. Scope

This taxonomy applies to:

- All production environments and supported non-prod environments
- Observability tools such as Splunk, Elastic, Grafana, AppDynamics, BigPanda, and ThousandEyes
- Alerts, enriched events, incident records, and dashboards
- Event pipelines integrating with ServiceNow or other ITSM platforms

---

## 3. Classification Dimensions

### 3.1 Technical Dimensions

| Dimension           | Description                                               | Example Values |
|---------------------|-----------------------------------------------------------|----------------|
| `layer`             | Where in the stack the event originated                   | `infrastructure`, `platform`, `application`, `integration`, `customer` |
| `service`           | Impacted technical or business service                    | `payments`, `loan-origination`, `user-auth` |
| `signal`            | Type of telemetry that produced the event                 | `log`, `metric`, `trace`, `synthetic`, `alert` |
| `cause`             | Contributing factor or root cause                         | `capacity`, `dependency`, `code`, `configuration`, `unknown` |
| `symptom`           | Observable behavior or state                              | `latency`, `error`, `timeout`, `degraded`, `no-data` |
| `impact`            | Business or operational severity                          | `high`, `medium`, `low`, `none` |
| `urgency`           | Time sensitivity for resolution                           | `immediate`, `next-business-hour`, `monitor-only` |
| `environment`       | Deployment context                                        | `prod`, `staging`, `dev`, `qa`, `dr` |
| `owner`             | Responsible team or squad                                 | `infra`, `platform-sre`, `payments-app` |
| `event_type`        | Nature of the event                                       | `threshold_breach`, `restart`, `anomaly_detected`, `deployment` |
| `recovery_state`    | Current status of the issue                               | `firing`, `resolved`, `stable`, `flapping` |
| `regulatory`        | Compliance implication                                    | `sox`, `pci`, `hipaa`, `gdpr`, `none` |
| `sla_slo`           | Linked SLO or SLA target                                  | `latency-95p`, `availability`, `submission-slo` |
| `ticket_id`         | Linked incident, change, or problem                       | `INC123456`, `CHG7890`, `PROB101` |
| `automation_action` | Automated or scripted remediation taken                   | `restarted-service`, `opened-ticket`, `none` |
| `escalation_policy` | Escalation logic used for notification                    | `pagerduty-primary`, `email-fallback` |

---

### 3.2 Business-Focused Dimensions

| Dimension         | Description                                                 | Example Values |
|-------------------|-------------------------------------------------------------|----------------|
| `business_kpi`    | Business outcome or metric related to the event             | `conversion-rate`, `approval-time`, `drop-off-rate` |
| `process_stage`   | Stage of a business process or customer journey             | `application-submitted`, `underwriting`, `funding`, `closing` |
| `customer_action` | What the customer was doing at the time                     | `submit-application`, `make-payment`, `upload-document` |
| `segment`         | Customer or business cohort affected                        | `retail`, `enterprise`, `vip`, `partner` |
| `outcome`         | Business result or state                                    | `approved`, `rejected`, `abandoned`, `in-progress` |

---

## Notes

- Business-focused dimensions may not be populated by default in all events.
- Enrichment pipelines (e.g., in Splunk, BigPanda) can add these based on known mappings or metadata.
- This taxonomy supports initiatives like business observability, KPI alerting, incident impact analysis, and executive reporting.

---

## 4. Example Event Classification

**Event**:  
"Payment API timed out during loan disbursement for a VIP customer."

**Classification Tags**:
- `layer`: application  
- `service`: payments  
- `signal`: log  
- `cause`: dependency  
- `symptom`: timeout  
- `impact`: high  
- `urgency`: immediate  
- `environment`: prod  
- `owner`: payments-app-team  
- `event_type`: threshold_breach  
- `recovery_state`: firing  
- `sla_slo`: loan-disbursement-slo  
- `business_kpi`: transaction-success-rate  
- `process_stage`: disbursement  
- `customer_action`: make-payment  
- `segment`: vip  
- `outcome`: failed  

---

## 5. Governance

| Item                | Details |
|---------------------|---------|
| **Maintained by**   | Observability Working Group (Platform + App + SRE) |
| **Review cadence**  | Quarterly, or when tools or business models change |
| **Feedback process**| Submit suggestions via `#observability`, email, or Jira |
| **Reference**       | [Tagging Quick Start Sheet](#) \| [Field Mapping Spec](#) |

---

## 6. Next Steps

- [ ] Socialize with key platform and application stakeholders  
- [ ] Integrate into BigPanda enrichment and dashboard filters  
- [ ] Tag current alerts and incidents using this model  
- [ ] Monitor tagging quality and iterate after 30 days  
- [ ] Create and maintain a shared glossary of tag values  
