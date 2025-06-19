# Enterprise Intelligence Extraction Framework v6

**General Document Analysis: Building a Comprehensive Intelligence Repository**

Analyze the **content that I will provide in my next message**. Your primary goal is to **extract and synthesize all information relevant to problem definition and system understanding**, specifically to build a comprehensive body of background context for the "Domain-Driven Discovery + Product Discovery Fusion" framework.

**Important: Provide ONLY the structured analytical output below, with no conversational preamble, closing remarks, or additional questions.**

**For each point of extracted information, explicitly label it as `[Directly Stated]` if it's explicitly found in the content, or `[Inferred/Contextual]` if it's derived through interpretation, correlation, or general knowledge applied to the content. If information for a category is missing, clearly state `[Information Missing]` for that specific bullet point or section within the category.**

Please thoroughly extract and summarize the following details.

---

## **Output Format Specification**

**Begin your analysis with the following header format:**

```
---
## DOCUMENT ANALYSIS: [Document Title from Source Reference]
---
```

Provide the analysis using the following structured format, filling in the details as per your extraction and labeling instructions:

---

### **Source References**
• **Original Document Title/Name:** [Title of the document, transcript, or descriptive name of the source material (e.g., "Q3 Planning Meeting Notes," "System X Onboarding Guide," "User Feedback Compilation 2025-06-18")]
• **Source Type:** [e.g., Confluence Page, SharePoint Document, Meeting Transcript, Email Thread, Screenshot, Internal Report, Slack Channel, Interview Notes]
• **Date of Content:** [Date the content was last updated, created, or the date of the meeting/discussion, if available]
• **Original Location (if applicable):** [Direct link to the digital source, or a clear path/description of where the original file/information is stored]

---

### **1. Purpose & Problem Statements (Relates to the 'Purpose Lens')**
• **Goals/Missions:** [Summary of explicit or implied goals, objectives, or mission statements related to the content's subject, with `[Label]` ]
• **Problems/Challenges:** [Detailed description of any explicit or implicit problems, challenges, pain points or inferred/contextual insights identified in the content, with `[Label]` ]
• **Desired Outcomes/Benefits:** [Explanation of the stated or implied desired outcomes or benefits if the described system/process works effectively or is improved, with `[Label]` ]
• **Downside/Opportunities:** [Any mentions of negative consequences if problems persist, or positive opportunities if they are addressed, with `[Label]` ]

---

### **2. Key Actors & Personas (Relates to the 'Persona + Journey Lens')**
• **Primary Users/Stakeholders:** [Comma-separated list of all identified roles, teams, or departments, with specific examples if available, with `[Label]` ]
• **Tasks/Responsibilities/Frustrations:** [Descriptions of their tasks, responsibilities, workflows, frustrations, rituals, or constraints from the content. Use separate bullet points for distinct, longer descriptions; combine short, related ones, with `[Label]` ]
• **Adjacent Actors:** [Comma-separated list of any implied or mentioned groups whose involvement is indirect but relevant, with `[Label]` ]

<!-- STRUCTURED DATA BLOCKS: Enable LLM chaining and programmatic entity extraction -->
**STAKEHOLDER_ENTITIES:** {{role: "[Role Name]", influence: "[High/Medium/Low]", decision_authority: "[High/Medium/Low/None]"}} with `[Label]`

---

### **3. Core Flows & Domain Concepts (Relates to the 'Flow & Domain Lens')**
• **Capabilities/Processes/Workflows:** [Details of core business capabilities, processes, or workflows, including their general sequence or purpose. Use separate bullet points for distinct, longer descriptions; combine short, related ones, with `[Label]` ]
• **Steps/Actions/Events:** [Comma-separated list of specific steps, actions, events, or command triggers explicitly mentioned, with `[Label]` ]
• **Key Business Terms/Concepts:** [Comma-separated list of central business terms or domain concepts, with brief definitions if provided or inferable. Example: "Account (user profile), Order (customer purchase), Ticket (support request)", with `[Label]` ]
• **Opaque/Manual/Fragile Processes:** [Indications or descriptions of processes identified as opaque, manual, fragile, or error-prone, with `[Label]` ]

<!-- STRUCTURED DATA BLOCKS: Process mapping for dependency analysis -->
**PROCESS_ENTITIES:** {{name: "[Process Name]", maturity: "[Basic/Intermediate/Advanced]", automation_level: "[Manual/Semi-Automated/Automated]", criticality: "[High/Medium/Low]"}} with `[Label]`

---

### **4. System Details & Signals (Relates to the 'Signal & System Lens')**
• **Systems/Tools/Technologies:** [Comma-separated list of specific systems, applications, tools, or technologies mentioned. Example: "CRM (Salesforce), ERP (SAP), Monitoring (Grafana)", with `[Label]` ]
• **Data/Metrics/Telemetry:** [Comma-separated list of references to existing data points, metrics, telemetry, or feedback mechanisms. Example: "Login success rate, User response times, User session duration", with `[Label]` ]
• **Business-Technical Alignment:** [How technical signals map to business KPIs, process flow visibility, customer impact correlation, business outcome measurement, with `[Label]`]
• **Observability Standardization:** [Template coverage, consistency patterns, manual vs automated insights, standardized approaches vs ad-hoc monitoring, with `[Label]`]
• **Decision Support Systems:** [What information different personas use to make decisions, reporting overhead, real-time vs batch insights, dashboard consumption patterns, with `[Label]`]
• **Cross-Domain Visibility:** [Inter-team dependencies, shared process understanding, communication effectiveness between technical and business teams, with `[Label]`]
• **Process Maturity Indicators:** [Manual vs systematic approaches, ownership clarity, accountability tracking, factory model adoption, with `[Label]`]
• **Traditional Observability Gaps:** [Missing telemetry, brittle automation, lack of system observability, challenges in understanding system behavior/reliability, with `[Label]`]
• **Current State/Performance:** [Descriptions of the current state or performance of the system/process (e.g., "slow," "unreliable," "manual," "automated"), with `[Label]` ]

<!-- STRUCTURED DATA BLOCKS: System inventory for integration mapping -->
**SYSTEM_ENTITIES:** {{name: "[System Name]", type: "[Monitoring/ERP/CRM/Database/etc]", criticality: "[Mission Critical/Important/Supporting]", observability_maturity: "[None/Basic/Intermediate/Advanced]", business_alignment: "[High/Medium/Low]"}} with `[Label]`

<!-- STRUCTURED DATA BLOCKS: Business observability assessment -->
**BOS_MATURITY_INDICATORS:** {{domain: "[Business Domain]", template_coverage: "[Full/Partial/None]", ownership_clarity: "[Clear/Unclear/Missing]", signal_alignment: "[Business/Process/System]"}} with `[Label]`

---

### **5. Strategic & Contextual Insights (Relates to the 'Strategic Lens')**
• **Business Drivers/Goals:** [Any overarching business drivers, strategic initiatives, or company-wide goals related to the topic. Use separate bullet points for distinct, longer descriptions; combine short, related ones, with `[Label]` ]
• **Constraints:** [Comma-separated list of explicit or implied technical, organizational, regulatory, or other constraints. Example: "Budget limitations, GDPR compliance, Legacy system dependencies", with `[Label]` ]
• **Organizational Fit:** [Indication of how the topic fits into the broader organizational landscape (core, supporting, or an edge case), with `[Label]` ]
• **Strategic vs. Commodity:** [Insights into what parts of this topic might be considered strategic versus commoditized, with `[Label]` ]
• **Interdependencies:** [Comma-separated list of any highlighted interdependencies with other teams, systems, or initiatives, with `[Label]` ]
• **Change Management Complexity:** [Organizational readiness for transformation, concurrent change impacts, stakeholder alignment challenges, with `[Label]`]
• **Enterprise Mandate Impact:** [How enterprise-level decisions affect local team autonomy, forced technology adoption, timeline pressures, with `[Label]`]

---

### **6. Technology & Platform Evolution**
<!-- PURPOSE: Capture enterprise transformation dynamics, migration complexity, and technology adoption risks -->
• **Platform Migrations:** [Technology transitions in progress or planned, migration scope, platform lifecycle changes, with `[Label]`]
• **Timeline Pressures:** [Mandated deadlines, migration windows, concurrent transformation conflicts, with `[Label]`]
• **Adoption Risk Factors:** [New/untested technologies at organization, team readiness gaps, training requirements, with `[Label]`]
• **Technology Dependencies:** [Systems affected by platform changes, integration breakage risks, downstream impacts, with `[Label]`]
• **Migration Complexity:** [Data model changes, configuration migrations, tooling transitions, operational disruption potential, with `[Label]`]
• **Concurrent Transformations:** [Multiple simultaneous changes, resource conflicts, complexity amplification factors, with `[Label]`]

<!-- STRUCTURED DATA BLOCKS: Technology transformation tracking -->
**TRANSFORMATION_ENTITIES:** {{source_tech: "[Current Technology]", target_tech: "[Target Technology]", timeline: "[Urgent/Planned/Exploratory]", risk_level: "[High/Medium/Low]", enterprise_mandate: "[Required/Recommended/Optional]"}} with `[Label]`

---

### **7. Entity Relationships & Dependencies** 
<!-- PURPOSE: Enable network analysis, dependency mapping, and impact assessment across repository -->
• **Stakeholder Relationships:** [Who reports to whom, collaboration patterns, decision dependencies, with `[Label]`]
• **System Integration Map:** [Data flows, API dependencies, shared databases, integration points, with `[Label]`]
• **Process Coupling:** [Sequential dependencies, parallel workflows, blocking relationships, handoff points, with `[Label]`]
• **Cross-Domain Dependencies:** [How different business domains interact, shared resources, coordination requirements, with `[Label]`]

---

### **8. Actionability & Priority Assessment**
<!-- PURPOSE: Enable triaging findings across hundreds of documents for strategic prioritization -->
• **Actionability Level:** [Immediately Actionable], [Requires Further Investigation], [Contextual Only] with `[Label]`
• **Strategic Priority:** [High Impact/High Urgency], [High Impact/Low Urgency], [Low Impact/High Urgency], [Low Impact/Low Urgency] with `[Label]`
• **Implementation Complexity:** [Quick Win], [Medium Effort], [Major Initiative] with `[Label]`
• **Resource Implications:** [Budget impact, headcount needs, technology requirements implied, with `[Label]`]
• **Migration Urgency vs Readiness:** [Urgent timeline with low readiness, adequate time with good readiness, rushed with high risk, well-planned with support, with `[Label]`]
• **Transformation Risk Assessment:** [High risk/high complexity, manageable risk/medium complexity, low risk/straightforward, unknown risk/needs analysis, with `[Label]`]

---

### **9. Cross-Reference & Knowledge Graph Markers**
<!-- PURPOSE: Build knowledge graph connections and prevent duplicate analysis -->
• **Related Documents:** [Documents that should be analyzed together, similar content sources, with `[Label]`]
• **Validation Requirements:** [Claims requiring verification with other sources, assumptions needing confirmation, with `[Label]`]
• **Pattern Indicators:** [Recurring themes, anomalies, potential systemic issues that appear across multiple contexts, with `[Label]`]
• **Conflicting Information:** [Any information that contradicts other known sources or seems inconsistent, with `[Label]`]

---

### **10. Unstructured Context & Emerging Patterns**
<!-- PURPOSE: Capture unknown unknowns and patterns that don't fit standard categories -->
• **Unusual Patterns:** [Anything that seems significant but doesn't fit standard categories, unexpected relationships or behaviors, with `[Label]`]
• **Implicit Assumptions:** [Unstated beliefs or assumptions underlying the content, cultural or organizational assumptions taken for granted, with `[Label]`]
• **Context Clues:** [References to external events, initiatives, or knowledge not explicitly defined, mentions of broader organizational context, with `[Label]`]
• **Organizational Signals:** [Cultural indicators, political dynamics, informal processes mentioned, power structures or influence patterns, with `[Label]`]
• **Emerging Themes:** [New concepts, evolving terminology, changing priorities mentioned, indicators of organizational evolution, with `[Label]`]
• **Historical References:** [Past attempts, lessons learned, previous failures or successes, institutional memory indicators, with `[Label]`]
• **Future Indicators:** [Planned changes, anticipated challenges, emerging requirements, strategic direction signals, with `[Label]`]

<!-- STRUCTURED DATA BLOCKS: Pattern discovery for continuous learning -->
**UNKNOWN_PATTERN_ENTITIES:** {{pattern_type: "[New Category]", frequency: "[Single/Multiple]", significance: "[High/Medium/Low]", domain: "[Technical/Business/Organizational]", investigation_needed: "[Yes/No]"}} with `[Label]`

---

### **11. Enterprise Evolution Context**
<!-- PURPOSE: Proactive capture of enterprise-specific emerging patterns -->
• **Regulatory Evolution:** [New compliance requirements, audit patterns, governance changes, regulatory pressure indicators, with `[Label]`]
• **Vendor Ecosystem Shifts:** [Tool consolidation, new market entrants, technology obsolescence, supplier relationship changes, with `[Label]`]
• **Organizational Structure Changes:** [Team reorganizations, responsibility shifts, new roles emerging, reporting structure modifications, with `[Label]`]
• **External Pressure Indicators:** [Industry trends, competitive pressures, customer expectation changes, market force impacts, with `[Label]`]
• **Innovation Signals:** [Pilot programs, experimental approaches, new methodologies being explored, technology adoption patterns, with `[Label]`]

---

### **12. Analysis Quality & Meta-Assessment**
<!-- PURPOSE: Build self-improving feedback loops and identify analysis gaps -->
• **Information Density:** [Rich context/Standard detail/Sparse information] with confidence assessment, with `[Label]`
• **Domain Novelty:** [Familiar territory/Adjacent domain/Unfamiliar space] - indicates need for specialized analysis, with `[Label]`
• **Analysis Confidence:** [High confidence in extraction/Medium confidence/Low confidence/Requires domain expert review], with `[Label]`
• **Critical Information Gaps:** [Missing context that would significantly change analysis, key stakeholders not mentioned, process steps unclear, with `[Label]`]
• **Follow-up Investigation Needs:** [Specific additional sources needed, expert consultation required, validation steps recommended, with `[Label]`]
• **Prompt Evolution Signals:** [Patterns suggesting new extraction categories needed, recurring themes not well captured by current structure, with `[Label]`]

---

**OBSERVABILITY_TAGS:** [Alert_Fatigue: High/Medium/Low/None], [Business_Criticality: Mission_Critical/Important/Supporting], [Automation_Potential: High/Medium/Low/Manual_Only], [Analysis_Novelty: Standard/Adjacent/Novel] with `[Label]`
