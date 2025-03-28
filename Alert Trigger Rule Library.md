# Alert Trigger Rule Library (v1.1)

**Version:** 1.1 
**Release Date:** 2025-03-28  
**Maintainer:** Observability Governance 
**Status:** Baseline for solicitation and reference

> Goal is to reach a baseline version of the Alert Trigger Rule Library. All future changes will be tracked as incremental versions. Use this version for training, tool alignment, governance reporting, and implementation planning.

---

## Supported Trigger Actions

Only the following standardized trigger actions are permitted to ensure clarity, scalability, and governance alignment:

1. **xMatters** – For paging/on-call escalation  
2. **ServiceNow Incident** – For structured incident management  
3. **Dashboard alert/visualization** – For contextual and passive alerting  
4. **Event suppression or enrichment** – For noise control and correlation logic  
5. **Email** – Discouraged; legacy use only under strict review  
6. **Audit trail / Governance queue** – For compliance, tuning, and quality improvement workflows

> All rules below conform to this trigger action model.

---

## Implementation Guidance

To operationalize this rule library across teams and platforms:

### 1. Ownership & Roles
- Assign each alert rule to a responsible **system owner or SRE team**.
- Designate a **rule steward** to review triggers quarterly.

### 2. Tool Alignment
- Map trigger actions to implementation in tools:  
  - `xMatters` integration in alert platform  
  - `ServiceNow` incident connector for auto-ticketing  
  - Dashboards configured in Splunk, Grafana, or ITSI  
  - Suppression/enrichment in BigPanda, ITSI, or custom logic pipelines

### 3. Governance Workflow
- Integrate alert lifecycle with change management:  
  - New alerts must be proposed via template  
  - Decommissioned alerts must be logged with rationale  
- Use the **Governance Queue** trigger for non-compliant alerts

### 4. Testing & Validation
- All alerts must include:  
  - Trigger simulation or historical proof  
  - Clear success/failure criteria  
  - Target service mapping and routing validation

### 5. Continuous Improvement
- Conduct quarterly reviews:  
  - High-frequency alert analysis  
  - Unused alert pruning  
  - Correlation rule effectiveness  
- Use **CI rules** (e.g., CI-002, CI-008) as feedback signals

### 6. Communication
- Maintain visibility:  
  - Share rule library and trigger summaries with teams  
  - Document alert behavior in playbooks and dashboards  
  - Integrate with observability onboarding/training

---

## Alert Trigger Rule Set
Rationale: Each alert pattern category is designed to address specific needs—whether it’s proactive monitoring, business impact, or improving the alerting process. The rationale behind each pattern is to ensure that alerts are timely, relevant, and actionable, which helps teams improve operational efficiency, prevent disruptions, and align technical performance with business goals.

### Metric-Based Alert Patterns
Rationale: Metric-Based Alert Patterns are built around specific system metrics, such as CPU usage, memory usage, or disk space. These metrics serve as key performance indicators for system health. By setting thresholds and triggering alerts based on metric deviations, these patterns provide teams with early warnings of potential resource exhaustion, allowing for timely intervention and prevention of system failures. These alerts are critical in maintaining system stability and performance.

#### Rule ID: GC-001
- **Name:** Single GC Threshold Breach  
- **Condition:** GC time exceeds threshold once  
- **Trigger Action:** dashboard_only  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** One-time GC spikes are usually self-recovering and do not require immediate attention. Avoids unnecessary incident volume.

#### Rule ID: GC-002
- **Name:** Sustained GC Warning  
- **Condition:** GC warning persisted for >15 minutes  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Sustained GC load may indicate early signs of memory pressure; early action may prevent incident escalation.

#### Rule ID: GC-003
- **Name:** GC + Memory Saturation  
- **Condition:** GC warning occurs with high memory usage  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Combined conditions raise risk of degraded performance or crash, warranting investigation.

#### Rule ID: GC-004
- **Name:** GC + Transaction Latency  
- **Condition:** GC warning occurs along with transaction latency spikes  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Indicates resource contention, leading to degraded transaction performance.

#### Rule ID: GC-005
- **Name:** GC Warnings During Off-Hours Only  
- **Condition:** GC warnings triggered outside of business hours  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** informational  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Might be related to scheduled maintenance or lower system load; requires monitoring.

#### Rule ID: GC-006
- **Name:** GC Alert + No Recent Deploy  
- **Condition:** GC alert raised but no recent deployment or code changes  
- **Trigger Action:** Dashboard alert + incident review  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** Alerts without recent changes may indicate resource or environmental issues.

#### Rule ID: GC-007
- **Name:** GC Warning Cleared After Auto-Recovery  
- **Condition:** GC warning automatically cleared within 15 minutes  
- **Trigger Action:** Suppressed (for future occurrences)  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Auto-recovery suggests the issue was temporary; no immediate action needed.

#### Rule ID: GC-008
- **Name:** GC + Spike in Thread Count or CPU Usage  
- **Condition:** GC warning raised in combination with increased thread count or CPU usage  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Indicates potential resource exhaustion that could affect service availability.

#### Rule ID: GC-009
- **Name:** GC Alert Suppressed via Known Exception Tag  
- **Condition:** GC event tagged with known exception rule `suppress_alert=true`  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Suppress known behavior from noisy endpoints or systems.

#### Rule ID: GC-010
- **Name:** GC Event Repeated > X Times in 24h  
- **Condition:** GC warning raised multiple times (e.g., > 5) within 24 hours  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Repeated GC warnings over a short time frame suggest an underlying problem that may need addressing.

---

## Transaction Latency Alert Patterns
Rationale: Transaction Latency Alert Patterns focus on measuring delays in critical business processes, such as payment processing or service requests. Latency is a key indicator of performance issues that can degrade user experience or disrupt business operations. These alerts allow teams to identify bottlenecks, take corrective actions before service degradation becomes visible to customers, and maintain high availability and smooth user experiences.

#### Rule ID: TX-001
- **Name:** High Latency, No Failures  
- **Condition:** Transaction latency exceeds threshold without error rate increase  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2, Tier 3  
- **Rationale:** May indicate slow downstream dependency; warrants analysis but not immediate paging.

#### Rule ID: TX-002
- **Name:** High Latency + Error Rate Spike  
- **Condition:** Transaction latency and error rate exceed thresholds  
- **Trigger Action:** xMatters + ServiceNow incident  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Indicates degraded user experience or possible outage; immediate intervention required.

#### Rule ID: TX-003
- **Name:** Persistent Latency Across Multiple Endpoints  
- **Condition:** Latency threshold exceeded on 3+ endpoints for >10 minutes  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Suggests systemic issue, not isolated blip; requires visibility and triage.

#### Rule ID: TX-004
- **Name:** High Latency During Business Hours  
- **Condition:** Latency spikes occur during peak business hours  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Business impact is higher during peak hours; needs quick intervention.

#### Rule ID: TX-005
- **Name:** Latency Increased by External Dependencies  
- **Condition:** Transaction latency spikes coincide with external API failures  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Points to dependencies outside the system; escalates accordingly.

#### Rule ID: TX-006
- **Name:** Latency Without Expected Load Increase  
- **Condition:** Latency spikes but load remains stable  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Indicates potential performance bottleneck that needs further monitoring.

---

## Composite Alert Patterns
Rationale: Composite Alert Patterns combine multiple conditions or signals to create more complex, higher-impact alerts. These patterns are used when multiple metrics need to be considered together, such as high latency combined with increased error rates, to provide a clearer indication of an impending issue. By correlating different signals, composite alerts allow teams to focus on more meaningful events, improving incident response and reducing the risk of missing critical issues that could impact system reliability.

#### Rule ID: CP-001
- **Name:** GC + High Latency + Transaction Errors  
- **Condition:** GC threshold breach + transaction latency spike + elevated error rate  
- **Trigger Action:** xMatters + ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Strong correlation of symptoms pointing to degraded service; requires immediate on-call response.

#### Rule ID: CP-002
- **Name:** CPU Saturation + Memory Pressure + Latency  
- **Condition:** CPU usage > 90% + memory usage high + latency increase  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Indicates potential for cascading system failure if not addressed.

#### Rule ID: CP-003
- **Name:** Drop in Business Flow + Backend Dependency Failures  
- **Condition:** Flow completion rate drops + API/dependency errors increase  
- **Trigger Action:** ServiceNow incident + escalation to product owner  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Suggests business impact due to underlying technical fault; cross-team awareness needed.

---

## Suppression Patterns
Rationale: Suppression Patterns focus on reducing alert noise by identifying and suppressing non-actionable or repetitive alerts. By suppressing known issues (e.g., noisy endpoints or transient failures), teams can avoid alert fatigue and focus on high-priority issues. This ensures that only relevant, actionable alerts are sent out, improving the signal-to-noise ratio and reducing the operational burden of handling false alarms.

### **1. Known Noisy Endpoints**

#### Rule ID: SP-001
- **Name:** Known Noisy Endpoint Suppression  
- **Condition:** Alerts from endpoints or systems that are tagged as **noisy** or **non-actionable** in historical data.  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Known noisy endpoints generate frequent alerts that do not require attention and contribute to alert fatigue.

---

### **2. Temporary Failures or Retries**

#### Rule ID: SP-002
- **Name:** Suppress Temporary Failures or Retries  
- **Condition:** Temporary network failures or retries that occur within a predefined time window (e.g., within 5 minutes).  
- **Trigger Action:** Suppressed  
- **Severity:** warning/informational  
- **Tier Applicability:** all  
- **Rationale:** Short-term issues (e.g., network blips or retries) that typically resolve on their own should not trigger alert storms.

---

### **3. Low-Priority System Alerts**

#### Rule ID: SP-003
- **Name:** Low-Priority System Alert Suppression  
- **Condition:** Alerts from systems or services that are categorized as low-priority or non-critical in the business context (e.g., non-prod environments).  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** Tier 3  
- **Rationale:** Non-production environments or low-impact systems do not require immediate intervention, and alerts can be suppressed to focus on high-priority systems.

---

### **4. Frequent or Recurring Alert Suppression**

#### Rule ID: SP-004
- **Name:** Flapping Alert Suppression  
- **Condition:** Alerts that toggle between triggered and cleared multiple times (e.g., more than 3 times in 15 minutes).  
- **Trigger Action:** Suppress repeated alerts  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** Frequent toggling or flapping is often an indicator of unstable conditions that should be investigated manually, not automatically escalated each time.

---

### **5. Expected Maintenance Window**

#### Rule ID: SP-005
- **Name:** Suppress Alerts During Maintenance Window  
- **Condition:** Alerts triggered during scheduled maintenance or planned downtime.  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Alerts generated during known maintenance periods should be suppressed to avoid unnecessary notifications.

---

### **6. Historical Anomalies or Known Issues**

#### Rule ID: SP-006
- **Name:** Suppress Known Issue Alerts  
- **Condition:** Alerts related to **historically known issues** (e.g., performance degradation in a specific service identified as a recurring issue) that are being addressed or managed.  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Known issues that have been acknowledged and are not likely to lead to significant business disruption should be suppressed to avoid generating unnecessary alerts.

---

### **7. Low Impact Environment Alerts**

#### Rule ID: SP-007
- **Name:** Suppress Alerts from Low-Impact Environments  
- **Condition:** Alerts from lower-priority or low-impact environments (e.g., sandbox, testing environments) that do not directly affect production or customer-facing services.  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** Tier 3  
- **Rationale:** Alerts from non-production environments do not require immediate action and can create unnecessary noise.

---

### **8. Low Severity Alerts**

#### Rule ID: SP-008
- **Name:** Low Severity Alerts Suppression  
- **Condition:** Alerts classified as **low severity** that do not require immediate resolution or intervention.  
- **Trigger Action:** Suppressed  
- **Severity:** warning/informational  
- **Tier Applicability:** all  
- **Rationale:** Low-severity alerts that do not pose immediate risks to the business or customer experience should be suppressed to minimize alert fatigue.

---

### **9. Repetitive Alerts for Same Issue**

#### Rule ID: SP-009
- **Name:** Suppress Repetitive Alerts for Same Issue  
- **Condition:** Repeated alerts for the same root cause or issue within a short period (e.g., same alert triggered more than 5 times in an hour).  
- **Trigger Action:** Suppressed  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** Repeated alerts for the same issue contribute to alert fatigue and are not useful if they represent the same underlying problem.

---

### **10. Non-Actionable Information Events**

#### Rule ID: SP-010
- **Name:** Suppress Non-Actionable Informational Events  
- **Condition:** Informational events with no actionable consequence (e.g., logs that simply confirm an event without triggering further action).  
- **Trigger Action:** Suppressed  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Informational events that do not provide additional value or trigger necessary action should be suppressed to focus on critical events.


---

## Business Observability Alert Patterns
Rationale: Business Observability Alert Patterns are tied to business KPIs and customer outcomes, focusing on providing visibility into how technical performance directly impacts the business. These alerts prioritize critical business flows, such as customer transactions or service-level expectations, allowing teams to connect technical alerts with business context. This helps prioritize actions that will directly improve customer satisfaction and business success.

### **1. Money or Dollar Value Related**

#### Rule ID: BO-001
- **Name:** Significant Drop in Revenue per Transaction  
- **Condition:** Average revenue per transaction falls below a defined threshold (e.g., 20% decrease within 24 hours).  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** A significant drop in revenue can indicate issues with pricing, promotions, or fraud.

#### Rule ID: BO-002
- **Name:** Large Order Volume without Payment Confirmation  
- **Condition:** More than 50 high-value orders (>$1000) are placed but no payment confirmation received in 15 minutes.  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** High-value orders without payment confirmation may signal fraud or payment gateway issues.

#### Rule ID: BO-003
- **Name:** Financial Transaction Failure Rate Exceeds Threshold  
- **Condition:** More than 5% of financial transactions fail within a given time window (e.g., 30 minutes).  
- **Trigger Action:** xMatters + ServiceNow incident  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Failure to process payments impacts cash flow and customer experience.

---

### **2. Customer Related**

#### Rule ID: BO-004
- **Name:** Customer Flow Drop-off Detected  
- **Condition:** Business flow reaches step A but does not progress to step B within threshold time  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Indicates a disruption in the customer journey (e.g., application not completed); critical for business impact visibility.

#### Rule ID: BO-005
- **Name:** Increased Customer Complaints  
- **Condition:** Customer complaints exceed a defined threshold (e.g., more than 100 complaints in an hour).  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** An increase in complaints may indicate product or service failure, or poor customer experience.

#### Rule ID: BO-006
- **Name:** Customer Retention Drop  
- **Condition:** Customer retention rate falls below 75% month-over-month.  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2  
- **Rationale:** Low retention can signal product dissatisfaction or increased competition.

---

### **3. User Related**

#### Rule ID: BO-007
- **Name:** High User Account Lockout Rate  
- **Condition:** More than 10% of users experience account lockout due to multiple failed login attempts in 1 hour.  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** High lockout rates may indicate either a security threat (brute force attack) or user experience issues (complex authentication).

#### Rule ID: BO-008
- **Name:** Drop in Active Users  
- **Condition:** Active user count drops by more than 30% compared to the previous week.  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2  
- **Rationale:** A sudden drop in active users may indicate issues with user interface, performance, or new feature adoption.

#### Rule ID: BO-009
- **Name:** Surge in New User Registrations  
- **Condition:** User registrations exceed 500 new accounts per hour, far above historical baseline.  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2  
- **Rationale:** A sudden surge could indicate marketing campaign success, but could also be a sign of a bot attack.

---

### **4. Legal Risk and Compliance Related**

#### Rule ID: BO-010
- **Name:** Privacy Policy Violation Detected  
- **Condition:** User data is accessed without required consent or beyond the scope of agreed usage.  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Violations could result in legal consequences, regulatory penalties, and damage to brand reputation.

#### Rule ID: BO-011
- **Name:** GDPR Non-Compliance Detected  
- **Condition:** Personal data of users within the EU is stored or processed outside of GDPR compliance standards (e.g., breach of data storage policy).  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Non-compliance with GDPR regulations can lead to fines, legal action, and loss of trust.

#### Rule ID: BO-012
- **Name:** Unauthorized Access to Sensitive Data  
- **Condition:** Unauthorized access is detected for sensitive data sets, such as credit card details or health records.  
- **Trigger Action:** ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** This could represent a major security breach and lead to legal and compliance consequences.

---

### **5. Operational Efficiency Related**

#### Rule ID: BO-013
- **Name:** Operational Process Bottleneck Detected  
- **Condition:** A key operational process (e.g., order fulfillment) exceeds expected processing time by more than 30%.  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2  
- **Rationale:** Bottlenecks can lead to delays, inefficiencies, and customer dissatisfaction.

#### Rule ID: BO-014
- **Name:** Resource Utilization Efficiency Drop  
- **Condition:** Resource utilization (e.g., server, storage) drops below 60% capacity utilization over a sustained period.  
- **Trigger Action:** ServiceNow incident (low priority)  
- **Severity:** informational  
- **Tier Applicability:** Tier 3  
- **Rationale:** Low utilization could suggest underused resources or inefficiencies in scaling.

#### Rule ID: BO-015
- **Name:** Employee Productivity Drop  
- **Condition:** Productivity of employees or teams drops by more than 20% within a week.  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning  
- **Tier Applicability:** Tier 2  
- **Rationale:** A drop in productivity may indicate issues with internal tools, workflow inefficiencies, or morale.

---

### **6. Business workflow Related**

#### Rule ID: BO-016
- **Name:** Missing Informational Milestone Event  
- **Condition:** Expected informational event (e.g., `loan_submitted`) not received within defined timeframe  
- **Trigger Action:** ServiceNow incident or dashboard alert  
- **Severity:** warning  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Absence of a known event may signify stalled process, system lag, or business flow interruption.

#### Rule ID: BO-017
- **Name:** Business KPI Anomaly Detected  
- **Condition:** Business metric (e.g., conversion rate, doc uploads) deviates from historical baseline  
- **Trigger Action:** ServiceNow incident (medium priority)  
- **Severity:** warning/exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Business KPIs reflect user success and financial impact; anomalies must be triaged.

---

## Continuous Improvement Alert Patterns
Rationale: Continuous Improvement Alert Patterns are designed to optimize alerting by identifying patterns and refining thresholds based on past incidents. The goal is to reduce alert fatigue, ensure alert relevancy, and improve the overall efficiency of monitoring systems. By reviewing high-frequency alerts, suppressing unnecessary notifications, and continuously improving correlation rules, organizations can ensure that their alerting system stays efficient, precise, and aligned with operational goals.

#### Rule ID: CI-001
- **Name:** High-Frequency Alert Source  
- **Condition:** Same alert source triggers > X times/day  
- **Trigger Action:** Dashboard + alert tuning review  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** Indicates poor alert threshold, missing suppression, or noise pattern.

#### Rule ID: CI-002
- **Name:** Alerts Closed Without Action  
- **Condition:** > Y% of alerts closed with no action in past 30 days  
- **Trigger Action:** Governance review ticket  
- **Severity:** informational  
- **Tier Applicability:** all  
- **Rationale:** Helps identify non-actionable alerts that contribute to fatigue.

---

## Domain-Specific Alert Patterns
Rationale: Domain-Specific Alert Patterns focus on unique business requirements in specific industries such as e-commerce, finance, healthcare, etc. These patterns are designed to monitor and alert based on key business processes that impact operational performance. By focusing on domain-relevant KPIs and behaviors, these alerts provide critical visibility into business performance, helping teams identify and address issues that directly affect customer experience and business outcomes.

### Financial Services

#### Rule ID: FS-001
- **Name:** Unusual Login Location
- **Condition:** User logs in from a new country or location.
- **Trigger Action:** ServiceNow incident (high priority)
- **Severity:** exception
- **Tier Applicability:** Tier 1
- **Rationale:** Possible security threat or fraud activity requiring immediate investigation.

#### Rule ID: FS-002
- **Name:** Failed Fund Transfer Attempts
- **Condition:** More than 3 failed fund transfers in a 30-minute window.
- **Trigger Action:** xMatters + ServiceNow incident
- **Severity:** warning
- **Tier Applicability:** Tier 1
- **Rationale:** May indicate an issue with the payment gateway or potential fraud.

#### Rule ID: FS-003
- **Name:** Loan Application Delay
- **Condition:** Loan approval process takes longer than 48 hours.
- **Trigger Action:** ServiceNow incident (medium priority)
- **Severity:** warning
- **Tier Applicability:** Tier 2
- **Rationale:** Delays could impact customer satisfaction and financial performance.

#### Rule ID: FS-004
- **Name:** Payment Gateway Failure
- **Condition:** Payment request fails for more than 5 users within 10 minutes.
- **Trigger Action:** xMatters + ServiceNow incident
- **Severity:** exception
- **Tier Applicability:** Tier 1
- **Rationale:** Direct impact on revenue generation and customer experience.

### Software as a Service (SaaS)

#### Rule ID: SA-001
- **Name:** Service Downtime Detection
- **Condition:** Service is unavailable for more than 5 minutes.
- **Trigger Action:** xMatters + ServiceNow incident
- **Severity:** exception
- **Tier Applicability:** Tier 1
- **Rationale:** Impacts user experience and business continuity.

#### Rule ID: SA-002
- **Name:** Unusual API Request Rate
- **Condition:** API request rate exceeds 1000 requests per minute.
- **Trigger Action:** ServiceNow incident (medium priority)
- **Severity:** warning
- **Tier Applicability:** Tier 2
- **Rationale:** Could indicate a DoS attack or unauthorized activity.

#### Rule ID: SA-003
- **Name:** Data Synchronization Failure
- **Condition:** Data sync fails between production and staging environments for > 1 hour.
- **Trigger Action:** ServiceNow incident (low priority)
- **Severity:** informational
- **Tier Applicability:** Tier 2
- **Rationale:** Non-critical but may cause data integrity issues if not addressed.

---

# Advanced Prediction Alert Patterns
Rationale: Advanced Prediction Alert Patterns leverage predictive analytics and machine learning to forecast issues before they occur, based on historical data and trends. This proactive approach ensures that potential issues can be mitigated early, reducing risk and improving system resilience. By acting on predicted problems, teams can optimize resource allocation and avoid unexpected disruptions.

#### Rule ID: AP-001
- **Name:** Forecasted SLO Breach  
- **Condition:** SLO is projected to breach within the next 6 hours based on current performance trends.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Enables proactive remediation to protect customer commitments.

#### Rule ID: AP-002
- **Name:** Predicted CPU Saturation  
- **Condition:** CPU usage trend predicts >90% usage within the next 2 hours.  
- **Trigger Action:** Dashboard alert + capacity planning task  
- **Severity:** warning  
- **Tier Applicability:** all  
- **Rationale:** Early intervention can avoid cascading resource issues.

#### Rule ID: AP-003
- **Name:** Predicted Memory Exhaustion  
- **Condition:** Memory usage trend indicates exhaustion within the next 4 hours.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** warning  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Prevent potential system crash or degraded performance due to resource exhaustion.

#### Rule ID: AP-004
- **Name:** Predicted Network Congestion  
- **Condition:** Network bandwidth usage trends indicate congestion will occur in the next 30 minutes.  
- **Trigger Action:** Dashboard alert + team notification  
- **Severity:** warning  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Proactively address network performance degradation to avoid impact on services.

#### Rule ID: AP-005
- **Name:** Predicted Latency Increase  
- **Condition:** Latency is expected to exceed threshold based on network traffic predictions for the next hour.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Allows teams to prepare for potential performance degradation before it occurs.

#### Rule ID: AP-006
- **Name:** Predicted Increase in Application Errors  
- **Condition:** Historical error patterns indicate an error spike will occur within the next 2 hours.  
- **Trigger Action:** xMatters + ServiceNow incident  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Provides early visibility into application issues before a full-scale failure.

#### Rule ID: AP-007
- **Name:** Predicted Service Degradation  
- **Condition:** Predictive model identifies trends that suggest a 50% decrease in service response time within 3 hours.  
- **Trigger Action:** ServiceNow incident + escalation  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Proactive monitoring and response to prevent full outages.

#### Rule ID: AP-008
- **Name:** Predicted Drop in Business Metric  
- **Condition:** A predictive model indicates a 10% drop in key business KPIs (e.g., conversions, sales) in the next 48 hours.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** warning  
- **Tier Applicability:** Tier 1  
- **Rationale:** Early insight into potential business impact, allowing teams to intervene before it becomes critical.

#### Rule ID: AP-009
- **Name:** Predicted Customer Flow Disruption  
- **Condition:** User flow analysis suggests that customer drop-off will exceed 15% in the next 6 hours.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Prevents disruptions in customer journeys that can lead to lost revenue and poor customer experience.

#### Rule ID: AP-010
- **Name:** Predicted Fraudulent Transactions  
- **Condition:** Predictive analysis detects anomalies in transaction patterns, indicating potential fraud.  
- **Trigger Action:** xMatters + ServiceNow incident (high priority)  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Early warning of fraud attempts allows immediate investigation and action.

#### Rule ID: AP-011
- **Name:** Predicted Account Compromise  
- **Condition:** Machine learning model detects an unusual pattern of login failures and IP address changes, indicating potential account compromise.  
- **Trigger Action:** ServiceNow incident + team notification  
- **Severity:** exception  
- **Tier Applicability:** Tier 1  
- **Rationale:** Allows for fast action to secure user accounts before widespread damage occurs.

#### Rule ID: AP-012
- **Name:** Predicted Scaling Needs  
- **Condition:** Predictive scaling model forecasts that system demand will exceed capacity in the next 2 hours.  
- **Trigger Action:** xMatters + scaling request to cloud resources  
- **Severity:** warning  
- **Tier Applicability:** Tier 1, Tier 2  
- **Rationale:** Ensures proactive resource scaling to prevent service degradation.

---
