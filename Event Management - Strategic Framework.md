# Strategic Framework for Event Management

## Purpose

This framework establishes a unified approach to event management across infrastructure, applications, platforms, and business services. It defines how events should be classified, enriched, routed, correlated, and retained to support operational awareness, incident response, and business observability.

---

## 1. Event Classification

All events must be categorized to drive appropriate routing and response:

| **Category**   | **Definition**                                                  | **Examples**                          |
|----------------|------------------------------------------------------------------|----------------------------------------|
| Informational  | Confirming normal or expected behavior, no action required      | `login_successful`, `batch_started`    |
| Warning        | Indicates threshold breach, unusual behavior, or potential risk | `CPU > 85%`, `retry detected`          |
| Exception      | Signifies failure, error, or degraded performance requiring action | `timeout`, `dependency_down`        |

---

## 2. Event Enrichment

Events should be enriched at ingestion with metadata that enhances correlation and routing:

| **Tag**         | **Purpose**                                      |
|------------------|--------------------------------------------------|
| `service`        | Logical or business service impacted             |
| `layer`          | Stack layer (e.g., app, infra, integration)      |
| `environment`    | Environment (e.g., prod, qa, dev)                |
| `owner`          | Responsible team or support group                |
| `business_kpi`   | Optional – related KPI if applicable             |
| `event_type`     | Nature (e.g., alert, start, anomaly, flow)       |
| `category`       | Informational, Warning, Exception                |

---

## 3. Event Routing and Retention Strategy

### Routing Guidelines
- **Exception and Warning events**: Always routed to alerting platforms and ITSM
- **Informational events**:
  - Retain upstream (e.g., Splunk) for context, dashboards, flow visualization
  - Route only **high-value informational events** to alert pipelines (e.g., BigPanda) with `category=informational` and `purpose=correlation_support`

### Retention Prioritization
- Prioritize events supporting:
  - Root Cause Analysis
  - Business observability and KPIs
  - Alert correlation timelines
- Suppress or exclude redundant events that add no correlation or business value

---

## 4. Correlation Strategy

Correlation engines (e.g., Splunk ITSI, BigPanda) rely on event quality:

- Use **correlation anchors**: Informational events marking state transitions (`job_started`, `checkout_initiated`)
- Group events based on shared metadata (`service`, `host`, `CI`, `business_process`)
- Create correlation rules that account for **presence or absence** of expected events

> Example: If `application_submitted` is not followed by `document_uploaded` within 10 mins → trigger drop-off alert.

---

## 5. Platform-Specific Guidance

### 🔷 Splunk ITSI
- Use **informational events** in service health scores, Glass Tables, KPI thresholds
- Enable **Episode Review** to include supporting events, not just alerts

> Splunk ITSI can operate on events directly from Splunk indexes, but benefits significantly from a structured event pipeline that enriches, filters, and classifies events before they are used in KPI evaluation, correlation searches, or Episode Review.

### 🔷 BigPanda
- Enrich informational events before routing
- Set `suppress_alert=true` when not directly actionable
- Use for **timeline enhancement** and **multi-signal correlation**

---

## 6. Cost and Performance Considerations

While informational events can increase data volume, they:
- Improve **mean time to detect and identify**
- Enable **full-fidelity RCA**
- Strengthen **business context**

> Note: Retaining informational events can increase storage by ~15%. Mitigate this via event tagging, routing filters, and view-level suppression.

Teams transitioning to this framework might initially experience increased event management complexity or alert fatigue; mitigate this by phased adoption, targeted training, and iterative tuning of correlation rules.

---

## 7. Governance

| **Area**                | **Guideline**                                             |
|-------------------------|------------------------------------------------------------|
| Ownership               | Event strategy governed by Observability Council           |
| Review cadence          | Quarterly or post-major incident                           |
| Tooling feedback loop   | Review suppression, correlation, and routing outcomes      |
| Operational education   | Teams must understand classification and tagging practices |

Quarterly reviews should assess correlation rule effectiveness, incident response efficiency, and event suppression accuracy (e.g., percentage of suppressed events that later proved relevant).

### Metrics & Measurement

Strategy success will be measured by tracking observability metrics such as Mean Time to Detect (MTTD), Mean Time to Resolve (MTTR), alert quality, and direct business KPI improvements, reviewed quarterly.

---

## 8. Summary

Event management is not just a pipeline—it is a strategy. Informational events are often overlooked, but when used purposefully, they significantly improve correlation, context, and insight.

A mature event management strategy:
- **Defines value-driven event retention**
- **Aligns observability with business outcomes**
- **Optimizes platform performance without sacrificing context**
