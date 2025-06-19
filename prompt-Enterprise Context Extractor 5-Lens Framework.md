### **Prompt Name:** `Enterprise Context Extractor (5-Lens Framework)`

**Description:** 
`Analyzes any provided text or image content (e.g., Confluence pages, meeting transcripts, SharePoint captures) to rigorously extract and categorize information across five key lenses: Purpose, Persona, Flow & Domain, Signal & System, and Strategic. The structured output builds a comprehensive body of context, optimized for subsequent LLM-driven synthesis and analysis within the Domain-Driven Discovery + Product Discovery Fusion framework.`
---

Output Format Example with Source Reference
---
### **Source Reference**
* **Original Document Title/Name:** [Title of the Confluence page, SharePoint document, meeting transcript, or descriptive name of the source material (e.g., "Q3 Planning Meeting Notes," "System X Onboarding Guide," "User Feedback Compilation 2025-06-18")]
* **Source Type:** [e.g., Confluence Page, SharePoint Document, Meeting Transcript, Email Thread, Screenshot, Internal Report, Slack Channel, Interview Notes]
* **Date of Content:** [Date the content was last updated, created, or the date of the meeting/discussion, if available]
* **URL/Location (if applicable):** [Direct link to the Confluence page, SharePoint file, or a clear path to where the original digital file is stored, if possible]
---

### 1. Purpose & Problem Statements (Relates to the 'Purpose Lens')
* **Goals/Mission:** [Summary of explicit or implied goals, objectives, or mission statements related to the content's subject.]
* **Problems/Challenges:** [Detailed description of any explicit or implicit problems, challenges, pain points, or inefficiencies identified in the content.]
* **Desired Outcomes/Benefits:** [Explanation of the stated or implied desired outcomes or benefits if the described system/process works effectively or is improved.]
* **Downsides/Opportunities:** [Any mentions of negative consequences if problems persist, or positive opportunities if they are addressed.]

---

### 2. Key Actors & Personas (Relates to the 'Persona + Journey Lens')
* **Primary Users/Stakeholders:** [List of all identified roles, teams, or departments, with specific examples if available.]
* **Tasks/Responsibilities/Frustrations:** [Descriptions of their tasks, responsibilities, workflows, frustrations, rituals, or constraints from the content.]
* **Adjacent Actors:** [Any implied or mentioned groups whose involvement is indirect but relevant.]

---

### 3. Core Flows & Domain Concepts (Relates to the 'Flow & Domain Lens')
* **Capabilities/Processes/Workflows:** [Outline of core business capabilities, processes, or workflows, including their general sequence or purpose.]
* **Steps/Actions/Events:** [Details of specific steps, actions, events, or command triggers explicitly mentioned.]
* **Key Business Terms/Concepts:** [List of central business terms or domain concepts, with brief definitions if provided or inferable.]
* **Opaque/Manual/Fragile Processes:** [Indications or descriptions of processes identified as opaque, manual, fragile, or error-prone.]

---

### 4. System Details & Signals (Relates to the 'Signal & System Lens')
* **Systems/Tools/Technologies:** [Specific systems, applications, tools, or technologies mentioned as being part of, or interacting with, the subject.]
* **Data/Metrics/Telemetry:** [References to existing data points, metrics, telemetry, monitoring, or feedback mechanisms.]
* **Observability Gaps/Brittle Automation:** [Explicit or implicit mentions of missing telemetry, brittle automation, lack of observability, or challenges in understanding system behavior/reliability.]
* **Current State/Performance:** [Descriptions of the current state or performance of the system/process (e.g., "slow," "unreliable").]

---

### 5. Strategic & Contextual Insights (Relates to the 'Strategic Lens')
* **Business Drivers/Goals:** [Any overarching business drivers, strategic initiatives, or company-wide goals related to the topic.]
* **Constraints:** [Explicitly stated or implied technical, organizational, regulatory, or other constraints.]
* **Organizational Fit:** [Indication of how the topic fits into the broader organizational landscape (core, supporting, edge case).]
* **Strategic vs. Commodity:** [Insights into what parts might be considered strategic versus commoditized.]
* **Interdependencies:** [Any highlighted interdependencies with other teams, systems, or initiatives.]
