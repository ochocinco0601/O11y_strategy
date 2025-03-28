# Team Guide: Event Categorization Framework

This guide helps teams consistently categorize events using a structured taxonomy that supports both technical operations and business observability. It enables better alert routing, response prioritization, and customer impact assessment.

---

## 1. Purpose

To provide a consistent and scalable approach for categorizing events that occur across infrastructure, applications, platforms, integrations, and customer-facing services. This framework aligns event metadata with business and technical priorities.

---

## 2. Event Categorization Matrix

| **Category**   | **Definition**                                         | **Examples**                                 | **Response Required?** | **Business Impact**      |
|----------------|--------------------------------------------------------|-----------------------------------------------|-------------------------|--------------------------|
| Informational  | Normal operations, expected system behavior            | Job completed, login successful               | No                      | None                     |
| Warning        | Early signs of potential issues                        | CPU > 85%, retry loops, anomaly detected      | Maybe – review context  | Potential risk           |
| Exception      | System or service failure with operational impact      | Payment API timeout, database full            | Yes – immediate action  | Definite or ongoing loss |

---

## 3. Event Classification Decision Tree

**Use the following decision steps to determine event category and enrichment tags:**

1. **Is the event part of expected, successful operations?**  
   → Yes → Categorize as **Informational**  
   → No → Proceed to Step 2

2. **Does it indicate a threshold breach, anomaly, or early warning without failure?**  
   → Yes → Categorize as **Warning**  
   → No → Proceed to Step 3

3. **Does it indicate active failure, degradation, or a breached SLA?**  
   → Yes → Categorize as **Exception**  
   → No → Proceed to Step 4

4. **Does the event relate to a business process, KPI, or customer experience?**  
   → Yes → Add **business context tags**  
   → No → Proceed with **technical tags only**

---

## 4. Tagging Reference

Apply relevant metadata to each event using the taxonomy below:

### 4.1 Core Technical Dimensions

| **Tag**          | **Purpose**                               | **Examples**                             |
|------------------|--------------------------------------------|-------------------------------------------|
| `layer`          | Where in the stack the event occurred      | `infrastructure`, `platform`, `application` |
| `service`        | Affected technical or business service     | `loan-origination`, `auth`, `payments`    |
| `signal`         | Type of telemetry signal                   | `log`, `metric`, `trace`, `synthetic`     |
| `cause`          | Contributing factor or failure cause       | `capacity`, `dependency`, `bug`           |
| `symptom`        | Observable issue or condition              | `latency`, `timeout`, `error`             |
| `impact`         | Severity of business or system effect      | `high`, `medium`, `low`                   |
| `urgency`        | Required response time                     | `immediate`, `next-business-hour`         |
| `environment`    | System environment                         | `prod`, `staging`, `dev`, `qa`            |
| `owner`          | Responsible team or function               | `infra`, `payments-app`, `sre-platform`   |
| `event_type`     | Nature of the event                        | `threshold_breach`, `restart`, `deployment` |
| `recovery_state` | Event condition status                     | `firing`, `resolved`, `flapping`          |

### 4.2 Business-Focused Dimensions

| **Tag**            | **Purpose**                                      | **Examples**                          |
|--------------------|--------------------------------------------------|----------------------------------------|
| `business_kpi`     | KPI or business metric tied to the event         | `approval-rate`, `conversion-time`     |
| `process_stage`    | Step in customer or business process             | `underwriting`, `funding`, `closing`   |
| `customer_action`  | What the customer was doing                      | `submit-application`, `make-payment`   |
| `segment`          | Customer or business group                       | `vip`, `retail`, `partner`, `refinance`|
| `outcome`          | Business result or state                         | `approved`, `rejected`, `abandoned`    |

### 4.3 Operational & Compliance Tags

| **Tag**              | **Purpose**                                     | **Examples**                          |
|----------------------|--------------------------------------------------|----------------------------------------|
| `sla_slo`            | Related SLA or SLO for tracking                  | `latency-95p`, `application-submission-slo` |
| `ticket_id`          | Associated incident or change record             | `INC123456`, `CHG78901`               |
| `automation_action`  | What remediation (if any) was executed           | `restarted-service`, `opened-ticket`  |
| `escalation_policy`  | Escalation handling strategy                     | `pagerduty-primary`, `email-only`     |
| `regulatory`         | Compliance or legal relevance                    | `sox`, `pci`, `gdpr`                  |

---

## 5. Example: Tagged Event

**Event**:  
"Customer loan disbursement failed due to payment service timeout."

**Tags**:
- layer: application  
- service: payments  
- signal: log  
- cause: dependency  
- symptom: timeout  
- impact: high  
- urgency: immediate  
- environment: prod  
- owner: payments-app-team  
- event_type: threshold_breach  
- recovery_state: firing  
- business_kpi: disbursement-success-rate  
- process_stage: disbursement  
- customer_action: make-payment  
- segment: vip  
- outcome: failed  
- ticket_id: INC120057  
- automation_action: none  

---

## 6. Responsibilities

- **Platform teams**: Enrich events at ingestion and routing layers  
- **App teams**: Classify events accurately during development and alert tuning  
- **SREs**: Validate tagging quality during incident reviews  
- **Business analysts**: Map business KPIs and process stages where applicable  

---

## 7. Reference Links

- [Internal Event Taxonomy Proposal](#)  
- [Quick Start Tagging Sheet](#)  
- [Service Catalog](#)  
- [Alert Enrichment Guide](#)  
- [Incident Response Handbook](#)
"""
