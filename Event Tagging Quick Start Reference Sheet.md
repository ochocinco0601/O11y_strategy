# Event Tagging Quick Start Reference Sheet

Use this sheet to quickly apply consistent tags to events across logs, metrics, alerts, traces, and incidents.

---

## 1. Core Technical Tags

| **Tag**       | **Purpose**                                 | **Example Values**                            |
|---------------|---------------------------------------------|------------------------------------------------|
| `layer`       | Where the event originated in the stack     | `infrastructure`, `platform`, `application`   |
| `service`     | Business or system service impacted         | `loan-origination`, `auth`, `payments`        |
| `signal`      | Type of telemetry that produced the event   | `metric`, `log`, `trace`, `synthetic`, `alert`|
| `cause`       | Likely contributor to the issue             | `capacity`, `dependency`, `code`, `unknown`   |
| `symptom`     | Observed system behavior                    | `latency`, `error`, `timeout`, `degraded`     |
| `impact`      | Business/operational severity               | `high`, `medium`, `low`, `none`               |
| `urgency`     | Time sensitivity for resolution             | `immediate`, `next-business-hour`             |
| `environment` | Deployment context                          | `prod`, `staging`, `qa`, `dev`                |
| `owner`       | Responsible team                            | `platform-sre`, `loan-app-team`               |
| `event_type`  | What type of event it is                    | `threshold_breach`, `restart`, `anomaly`      |
| `recovery_state` | Status of the event                      | `firing`, `resolved`, `stable`                |

---

## 2. Business Context Tags

| **Tag**           | **Purpose**                                          | **Example Values**                       |
|-------------------|------------------------------------------------------|------------------------------------------|
| `business_kpi`    | Metric or KPI tied to business impact                | `conversion-rate`, `approval-time`       |
| `process_stage`   | Stage of customer journey or business process        | `underwriting`, `application-submitted`  |
| `customer_action` | What the customer was trying to do                   | `submit-application`, `make-payment`     |
| `segment`         | Customer or business group affected                  | `vip`, `refinance`, `retail`, `partner`  |
| `outcome`         | Result of the process or customer interaction        | `approved`, `abandoned`, `in-progress`   |

---

## 3. Operational Tags

| **Tag**             | **Purpose**                                 | **Example Values**                   |
|---------------------|---------------------------------------------|--------------------------------------|
| `sla_slo`           | Linked service-level goal                   | `api-availability`, `latency-95p`    |
| `ticket_id`         | Associated incident/change/problem          | `INC12345`, `CHG67890`               |
| `automation_action` | Remediation applied (automated/manual)      | `restarted-service`, `opened-ticket` |
| `escalation_policy` | Who gets notified and how                   | `pager-duty-primary`, `email-only`   |
| `regulatory`        | Compliance relevance                        | `pci`, `gdpr`, `sox`, `none`         |

---

## 4. Tagging Guidelines

- **Start with what you know**: Focus on `layer`, `service`, and `signal` first.
- **Use existing metadata**: Pull tags from hostnames, namespaces, telemetry payloads, and incident fields.
- **Don’t guess**: Leave unknown tags blank or use `unknown`.
- **Enrich later**: Automation pipelines can fill in `owner`, `sla_slo`, and `segment` based on known mappings.
- **Consistency beats completeness**: It’s better to have 3 consistent tags than 10 inconsistent ones.

---

## 5. Example: Tagged Event

**Event**: "Customer payment failed due to service timeout"

**Tags**:

- layer: application  
- service: payments  
- signal: log  
- cause: dependency  
- symptom: timeout  
- impact: high  
- environment: prod  
- owner: payments-team  
- business_kpi: transaction-success-rate  
- process_stage: payment-submission  
- customer_action: make-payment  
- segment: vip  
- outcome: failed  
- ticket_id: INC009876  

---

## 6. Resources

- [Event Taxonomy Overview](#)  
- [Field Mapping for BigPanda and Splunk](#)  
- [Alert Enrichment Examples](#)  
- [Playbooks by Service](#)
