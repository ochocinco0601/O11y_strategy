# Position Paper: The Strategic Value of Informational Events in Event Management with Splunk ITSI

## Executive Summary

Informational events, though non-actionable, significantly enhance service health monitoring, incident correlation accuracy, and business observability within Splunk ITSI. Rather than universally dropping them, organizations should strategically tag, retain, and leverage these events to optimize operational visibility and decision-making effectiveness.

---

## Purpose

This paper evaluates the importance of retaining informational events in enterprise event pipelines and positions their use as a critical enabler of accurate service health scoring, correlation, and business observability within **Splunk ITSI**. While dropping these events may appear beneficial from a noise-reduction or cost-optimization standpoint, doing so may have significant trade-offs in terms of situational awareness, diagnostic depth, and business context.

---

## Background

Event management systems like Splunk ITSI are designed to collect, enrich, correlate, and route events to facilitate intelligent alerting and service-level monitoring. Events are typically categorized as:

- **Informational** – Signals of successful operations or expected system activity.
- **Warning** – Indications of a threshold breach or potential degradation.
- **Exception** – Failures, SLA breaches, or disruptions that require action.

Informational events, by definition, do not require direct action. However, their role in enabling insight, context, and accurate service state modeling is often underestimated.

---

## The Case for Retaining Informational Events

### 1. Enabling Accurate Correlation and Episode Review

Splunk ITSI relies on **Episode Review** and **correlation search logic** to group related events into meaningful episodes. Informational events can:
- Act as **anchors** or **state transitions** in rule logic.
- Help **validate** the relevance of adjacent warnings or exceptions.
- Improve **event grouping fidelity**, reducing false positives or missed correlations.

> Example: An `order_submitted` informational event may improve the signal confidence of a downstream `payment_timeout` exception by providing a known user journey checkpoint.

---

### 2. Supporting Flow-Based and Business Observability

Informational events frequently map to **business process milestones** (e.g., “loan application received”, “document uploaded”) that are not system failures but are essential to:
- Understand service **health beyond infrastructure**.
- Identify **conversion drop-offs** and **throughput bottlenecks**.
- Build **Glass Tables** that represent full business flows, not just error points.

Dropping these events would diminish visibility into customer experiences and introduce blind spots in service health dashboards.

---

### 3. Improving Root Cause Analysis (RCA) and Post-Incident Review

During RCA and retrospective analysis, informational events:
- Provide **contextual breadcrumbs** of what was working before failure.
- Help confirm that **expected behavior did not occur**, which is itself a key data point.
- Enhance timeline reconstruction and visibility in **Notable Events Review**.

> Absence of an expected informational event (“batch_job_started”) may itself be the trigger for an incident.

---

### 4. Enabling Advanced Use Cases in ITSI

Splunk ITSI correlation searches and KPI logic can be configured to:
- Use informational events as **conditional inputs** (e.g., “if X is seen and Y is not within 5 mins…”).
- Track **non-error flow completion** and correlate it with exceptions.
- Highlight **business-impacting patterns** that don’t produce traditional alerts.

This flexibility is a competitive strength of ITSI—and is best realized when event pipelines preserve informational data.

---

## Counterpoint: The Argument for Dropping Informational Events

Some operational strategies suggest dropping informational events to:
- Reduce data ingestion and storage cost
- Minimize visual or processing noise
- Focus correlation rules only on actionable data

While valid, this position assumes a narrow, alert-centric model that doesn’t support modern business observability needs or service-aware incident detection.

---

## Recommended Approach: Retain and Enrich Select Informational Events

Rather than dropping all informational events, organizations should:
1. **Tag events explicitly** as `category=informational`, with optional sub-tags like `purpose=correlation_support` or `business_kpi_marker`.
2. **Route or suppress based on purpose**, not just severity (e.g., suppress in dashboards but retain in timelines).
3. **Use ITSI correlation searches** that filter or leverage these events intentionally rather than ignoring them by default.

While selectively retaining informational events can increase storage requirements by approximately 15%, tagging and routing strategies can mitigate storage overhead by prioritizing retention based on defined business and operational value.

---

## Conclusion

Informational events are not noise—they are **signals without alarms**. They provide continuity, meaning, and structure to observability data and unlock capabilities within Splunk ITSI that go beyond alerting. Removing them universally risks undercutting the value of correlated incidents, service insights, and business observability.

The strategic position, therefore, is not to drop informational events, but to **enrich, tag, filter, and use them purposefully** in alignment with the maturity of event management and observability practices.

---

## Appendix: Examples of Informational Events with Operational Value

| Event Name              | Description                               | Value in ITSI                                      |
|-------------------------|-------------------------------------------|----------------------------------------------------|
| `loan_application_received` | Start of user flow                     | Supports funnel analysis, customer journey tracking |
| `document_uploaded`     | Expected process step                     | Missing upload could explain later SLA breach       |
| `batch_job_started`     | Operational marker                        | Missing marker = failed trigger or misconfigured job|
| `order_submitted`       | Completion of customer action             | Used to correlate and enrich downstream errors      |
