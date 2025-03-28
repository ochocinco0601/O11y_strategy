# Updated Event Taxonomy for Technical and Business Observability

This taxonomy supports both system-level and business-level event classification to enable effective monitoring, alerting, triage, and customer impact analysis.

---

## 1. Technical Dimensions

| Dimension           | Description                                                 | Example Values |
|---------------------|-------------------------------------------------------------|----------------|
| `layer`             | Where in the stack the event occurred                       | `infrastructure`, `platform`, `application`, `integration`, `customer` |
| `service`           | System or business service impacted                         | `payments`, `loan-origination`, `identity-verification` |
| `signal`            | Type of telemetry that generated the event                  | `log`, `metric`, `trace`, `synthetic`, `alert` |
| `cause`             | Contributing factor or root cause                           | `capacity`, `dependency`, `bug`, `configuration`, `unknown` |
| `symptom`           | Observable behavior or state                                | `latency`, `error`, `timeout`, `degraded`, `no-data` |
| `impact`            | Level of business or operational impact                     | `high`, `medium`, `low`, `none` |
| `urgency`           | Response time sensitivity                                   | `immediate`, `next-business-hour`, `monitor-only` |
| `environment`       | Environment context                                         | `prod`, `staging`, `dev`, `qa`, `dr` |
| `owner`             | Responsible team                                            | `infra`, `sre`, `payments-team` |
| `event_type`        | Nature of event                                             | `threshold_breach`, `restart`, `deployment`, `anomaly_detected` |
| `recovery_state`    | Current status of the condition                             | `firing`, `resolved`, `stable`, `flapping` |
| `regulatory`        | Compliance implication                                      | `sox`, `pci`, `gdpr`, `none` |
| `sla_slo`           | Associated service-level target                             | `latency-95p`, `availability`, `application-submission-slo` |
| `ticket_id`         | Linked incident or change record                            | `INC123456`, `CHG78901` |
| `automation_action` | Automated remediation applied                               | `restarted-service`, `opened-ticket`, `none` |
| `escalation_policy` | Escalation or notification logic                            | `pagerduty-primary`, `email-only` |

---

## 2. Business-Focused Dimensions

| Dimension         | Description                                                   | Example Values |
|-------------------|---------------------------------------------------------------|----------------|
| `business_kpi`    | Business outcome or metric related to the event               | `conversion-rate`, `approval-time`, `abandonment-rate`, `funding-volume` |
| `process_stage`   | Stage in a business process or customer journey               | `application-submitted`, `underwriting`, `funding`, `closing` |
| `customer_action` | What the customer was doing at the time                       | `submit-application`, `make-payment`, `upload-document` |
| `segment`         | Customer or business segment impacted                         | `vip`, `retail`, `partner`, `refinance` |
| `outcome`         | Result or state from a business perspective                   | `approved`, `rejected`, `abandoned`, `in-progress` |

---

## Notes

- Business-focused dimensions may not be populated by default in all events.
- Enrichment pipelines (e.g., in Splunk, BigPanda) can add these based on known mappings or metadata.
- This taxonomy supports initiatives like business observability, KPI alerting, incident impact analysis, and executive reporting.
