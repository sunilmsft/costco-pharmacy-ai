# Costco Pharmacy - Technology and Integration Q&A

## Purpose

Prepare for high-level questions about how the proposed guided pharmacy experience could integrate with existing systems, what complexity may be involved, and how the concept could be de-risked without committing prematurely to a specific platform, model, cloud, or architecture.

This document is an outside-in preparation aid, not a proposed technical design.

## Core positioning

Use this response when asked what technology the solution requires:

"I intentionally kept the concept platform-agnostic. The first decision is not which model or cloud to use. It is which member outcome we want to improve, which existing systems need to participate, and what level of integration is justified. The implementation should align with Costco's approved architecture, security standards, technology partners, and operating model."

## What Technology Is Behind the Prototype?

“The prototype is a lightweight browser-based concept built with standard web technologies: HTML, CSS, and JavaScript.

It uses scripted, state-driven interactions and sample data, so there is no live AI model, backend, database, or Costco system integration behind it today.

I designed the member experience and used VS Code and GitHub Copilot to help implement and iterate on it. GitHub Copilot was a development accelerator; it is not part of the runtime experience.

The production technology would depend on which member journey Costco chooses to validate, which systems need to participate, and what level of integration and governance is justified.”

### Is the Prototype Actually Using AI?

“Not in the current runtime. The prototype simulates the intended experience so we can validate the member journey before choosing models, integrations, and architecture.

Some parts of a production experience may benefit from a language model, such as interpreting natural-language intent. Other parts—particularly clinical guidance and consequential actions—should rely on approved content, structured data, deterministic workflows, explicit confirmation, and appropriate human oversight.”

### Why Wasn’t a Live AI Model Connected?

“I wanted to validate whether the journey creates value first, rather than creating the appearance of a technically finished solution.

A model can make an interaction appear intelligent quickly, but the harder product questions are whether the journey is useful, which data can be used, where the clinical and operational boundaries sit, and which integrations are justified.”

### What Would a Production Version Require?

“A production version would separate the conversational experience from the systems that provide authoritative information and execute actions.

Depending on the selected journey, it could require identity and consent, approved clinical content, Costco APIs and workflows, deterministic execution for consequential actions, explicit confirmation, pharmacist or staff handoff, monitoring, auditability, and governance.

The final model, cloud, or platform should not be selected until the member outcome and required system participation are understood.”

### Simple Explanation of HTML, CSS, and JavaScript

Private explanation, not a required spoken answer:

- HTML = structure
- CSS = appearance and layout
- JavaScript = behavior and interaction

Think of a webpage like a house:

- HTML is the structure: walls, rooms, and doors.
- CSS is the appearance: paint, spacing, fonts, colors, and layout.
- JavaScript is the behavior: lights turning on, doors opening, and buttons responding.

### Wording Caution

Do not say:

“GitHub Copilot created the prototype.”

Prefer:

“I designed the experience and used GitHub Copilot as a development accelerator to help implement and iterate on it.”

## Thirty-second integration response

"The integration depth would increase gradually. Guide can begin by using approved information and connecting members to existing workflows. Assist may require authentication, approved context, and APIs that reduce repeated entry while preserving member confirmation. Anticipate would require permitted events or signals, consent, monitoring, and stronger governance. The reason for the Crawl-Walk-Run model is that we should not take on deeper integration until the earlier phase demonstrates value and operational readiness."

## Integration depth by phase

### Crawl - Guide

Primary behavior:
Help the member find the correct option, workflow, or person.

Potential integration:
- Approved public or internal content
- Workflow links
- Routing rules
- Basic session context
- Human handoff
- Telemetry and feedback

Typical characteristics:
- Lower integration complexity
- Public or unauthenticated scenarios may be possible
- Primarily read-only
- Does not perform the transaction
- Useful for initial learning

### Walk - Assist

Primary behavior:
Help the member complete more of the task while preserving member review and confirmation.

Potential integration:
- Identity and authentication
- Approved member or prescription context
- Existing APIs
- Prefilled forms
- Workflow status
- Context-rich handoff
- Audit trail
- Explicit member confirmation

Typical characteristics:
- Authenticated and contextual
- More integrated with existing workflows
- May reduce repeated data entry
- Deterministic systems should execute important actions
- Member remains in control

### Run - Anticipate

Primary behavior:
Surface a timely and relevant next need before the member searches for it.

Potential integration:
- Permitted events and signals
- Preference and consent management
- Notification systems
- Business rules
- Proactive orchestration
- Monitoring and evaluation
- Stronger governance and escalation

Typical characteristics:
- Highest integration and operating complexity
- Requires proven value and trust
- Must be permission-based
- Requires careful relevance controls
- Should not create unnecessary outreach or confusion

## Logical architecture

Describe the solution using logical layers rather than vendor products.

### 1. Member experience layer

Possible channels:
- Website
- Mobile application
- Conversational interface
- Voice
- Existing Costco-owned member channels

Responsibility:
Present guidance, collect intent, preserve member control, and connect the member to the appropriate workflow or person.

### 2. Guidance and orchestration layer

Responsibility:
- Understand member intent
- Manage conversational or journey context
- Apply deterministic business rules
- Select the appropriate workflow
- Decide when human help is required
- Preserve progress across the journey

### 3. Integration layer

Responsibility:
Connect through approved APIs, services, or events to existing systems such as:
- Identity
- Prescription transfer
- Refill
- Immunization
- Status
- Scheduling
- Member support
- Pharmacy staff tools

### 4. Trust, safety, and human-support layer

Responsibility:
- Authentication
- Authorization
- Consent
- Least-privilege access
- Member confirmation
- Privacy controls
- Auditability
- Clinical boundaries
- Pharmacist escalation
- Graceful fallback

### 5. Measurement and operations layer

Responsibility:
- Telemetry
- Explicit feedback
- Helpful Response Rate
- Completion and effort
- Business outcomes
- Handoff quality
- Operational monitoring
- Evaluation
- Incident handling
- Content and rule maintenance

## Likely questions and suggested responses

### How difficult would the integration be?

"It depends primarily on the availability and maturity of the existing APIs, identity model, workflow systems, and operational ownership. I would avoid estimating before understanding those dependencies. The phased approach lets us begin with a bounded scenario, learn where the real constraints are, and deepen the integration only when the value supports it."

### Are you proposing that AI directly access pharmacy systems?

"Not by default. Access should be limited to the minimum information required for the selected scenario through approved interfaces and permissions. Early phases could remain read-only or route into existing workflows. Actions that change data should use deterministic workflows, explicit member confirmation, and an auditable record."

### What technology, model, or cloud would this use?

"That should be governed by Costco's existing standards and approved platforms. The experience design should not depend on one model, cloud, or provider. The architecture should allow Costco to use its approved infrastructure, integration patterns, security controls, and technology partners."

### Would this replace current pharmacy systems?

"No. The concept is intended to complement and connect existing capabilities. The member may still end in the same refill, transfer, immunization, scheduling, or support workflow. The opportunity is to improve the journey into and across those workflows."

### What happens when the experience is wrong or unavailable?

"The experience needs graceful fallback from the beginning. It should communicate uncertainty, preserve progress where possible, and connect the member to the right staff member with useful context. It should never become the only route to pharmacy support."

### What Happens with an Emergency or an Unsupported Request?

“The prototype includes basic boundary behavior for these situations.

Potential medical-emergency language does not enter a normal pharmacy journey. The experience displays a clear emergency warning, directs the person to call 911 or the appropriate local emergency service, and explains that they should not wait for the chat or rely on Costco Pharmacy for emergency care.

Requests outside the supported pharmacy scope receive a clear boundary response and are redirected toward the pharmacy topics the concept supports.

In production, those behaviors would require Costco-approved safety policies, evaluation, localization, monitoring, escalation rules, and ongoing governance.”

#### Private prototype reference

The current concept demonstrates:

- emergency phrase detection
- clear emergency-service direction
- a direct emergency-call action
- no attempt to diagnose or continue a pharmacy workflow
- a graceful scope response for unrelated questions
- supported options for general medication information and pharmacy-related questions remaining available

The current behavior is illustrative, not a complete production safety system. It does not diagnose or assess medical severity. Production behavior would require broader testing and approved policies, and emergency localization would need to support the appropriate local emergency number. This branch is supporting evidence of responsible product design, not part of the planned main live demo.

#### Optional detail

“Responsible AI was one of my focus areas at Microsoft, so I intentionally treated boundaries, escalation, failure behavior, and human oversight as product requirements even in the concept prototype.”

### How would member and pharmacy data be protected?

"Through least-privilege access, approved data sources, authentication, consent where required, encryption, auditability, retention controls, and clear restrictions on what information may be used for each scenario. The detailed design would need to align with Costco's privacy, security, compliance, clinical-governance, and Responsible AI requirements."

### Would this be built or purchased?

"I would separate the member experience and operating model from the underlying technology decision. Costco may already have approved platforms or capabilities that can support parts of this. Discovery should identify what can be reused, where integration is required, and where a partner or custom capability is justified."

### How long would this take?

"I would not give a responsible timeline without understanding the selected scenario, existing systems, API readiness, security reviews, and operational ownership. I would first define a bounded phase with clear dependencies and success criteria, then produce a more informed estimate."

### What operating responsibilities would need to be assigned?

"That needs to be part of the design, not an afterthought. Ownership would be required for content, workflow rules, evaluation, monitoring, escalation, incidents, and change management. The appropriate owners would depend on Costco's existing operating model."

## Discovery questions to ask Costco

### Current systems and integration

- Which systems currently own the member and prescription workflows shown in the concept?
- Are those capabilities available through APIs, events, or an approved integration layer?
- Which workflows are public, authenticated, or staff-assisted?
- Are there existing orchestration, search, conversational, or AI capabilities that should be reused?

### Identity, privacy, and consent

- What identity patterns are used for authenticated pharmacy experiences?
- What information may be carried between workflows?
- Which actions require explicit member confirmation?
- What consent and preference-management patterns already exist?
- What retention and audit requirements apply?

### Operations and human support

- Where do members most often leave self-service and contact the pharmacy?
- What context can currently be carried into a staff handoff?
- Who owns workflow content, routing rules, and escalation paths?
- Who would monitor quality, incidents, and operational performance?
- What fallback paths must always remain available?

### Priorities and sequencing

- Which member or business outcome is the highest priority?
- What is the lowest-risk scenario that would still produce meaningful learning?
- Which integration dependency is likely to be the greatest constraint?
- What evidence would Costco require before expanding the experience?

## Audience Preparation Map

This section is private meeting preparation and must not be copied into the external-facing guide.

| Audience member | Likely lens | What may matter most | What to demonstrate | Questions to invite | Topics to avoid overclaiming |
| --- | --- | --- | --- | --- | --- |
| Evan | Visible impact; improvement metrics; practicality; speed to learning; tangible demonstrations | What visibly improves for the member; how improvement will be measured; whether the approach can start small; whether the concept feels actionable rather than theoretical | Clear before-and-after member journey; measurable outcomes; evidence gates; bounded pilot; prototype scenarios | "Which outcome would matter most to you?"; "Which scenario would provide the strongest initial signal?"; "What evidence would you want to see before expanding?" | Internal architecture; delivery timeline; platform choice; exact business impact without a baseline |
| Brian | Pharmacy workflow realism; member safety; operational practicality; pharmacist judgment; member and staff experience | Whether the scenarios reflect real pharmacy needs; where human or pharmacist involvement is required; whether the workflow oversimplifies pharmacy operations; whether the proposed experience could create confusion or additional workload | Clear boundaries; intentional human handoff; existing workflows remain authoritative; important decisions remain with pharmacy professionals; graceful fallback | "Where would this workflow require more pharmacy nuance?"; "Where should pharmacist judgment enter the experience?"; "Which member questions create the most avoidable friction today?" | Clinical advice; pharmacist workflow details not validated with Costco; regulatory assumptions; claims that automation should replace pharmacy staff |
| Tuan | Architecture; integration; system boundaries; identity; APIs; data flow; operational ownership | Which systems participate; whether integrations are read-only or transactional; what existing capabilities can be reused; how context moves between workflows; reliability, fallback, and support ownership | Platform-agnostic logical architecture; phased integration depth; minimum necessary access; existing systems remain systems of record; deterministic execution for important actions; auditability and graceful fallback | "What existing integration patterns would this need to align with?"; "Which capabilities could be reused rather than recreated?"; "Where do you expect the most significant integration constraint?"; "What context can safely move across workflows today?" | API availability; specific cloud or model provider; existing system capabilities; integration complexity or timing without discovery |
| Payod | Responsible AI; governance; data boundaries; monitoring; auditability; consent; escalation | How the experience is governed; what data is available to the experience; how incorrect or unsafe responses are handled; member control and consent; evaluation and ongoing monitoring; clear human escalation | Responsible AI throughout the lifecycle; least-privilege access; explicit member confirmation; boundary adherence; correct escalation; auditability; monitoring and evaluation; ability to stop or reduce capability | "Which governance requirements should shape the first phase?"; "What evaluation and monitoring standards would be required?"; "Which data or decision boundaries should remain explicit?"; "What evidence would be required before increasing capability?" | Compliance approval; governance readiness; data access permissions; claims that guardrails eliminate all risk |

Meeting behavior note:
When a question is difficult to understand, use:
"Let me play that back to make sure I understood the question correctly."

## Question Mapping Table

| Possible question | Likely audience lens | Best place to address it | Concise response | Follow-up question | Keep in main story or backup |
| --- | --- | --- | --- | --- | --- |
| What does the integration look like? | Evan; Tuan | Slide 5 | It starts with a bounded, phased model: Guide connects to approved information and workflows, Assist adds authenticated context and workflow support, and Anticipate would require signals, consent, and stronger governance. | "Which phase would you want to unpack first?" | Main story |
| How difficult would integration be? | Tuan; Evan | Slide 5 | It depends on existing APIs, identity, workflow ownership, and operating readiness. I would not estimate until those dependencies are known. | "Which dependency is most uncertain today?" | Main story |
| Which existing systems would be involved? | Tuan; Brian | Slide 5 | The exact systems would depend on the chosen scenario, but likely participants include identity, workflow, status, support, and pharmacy staff tools. | "Which workflow owns the member journey today?" | Main story |
| Does AI directly access pharmacy systems? | Tuan; Payod | Slide 4 | Not by default. Access should be limited to the minimum required through approved interfaces, with deterministic actions, explicit confirmation, and auditability where needed. | "Which actions would need to remain system-driven rather than model-driven?" | Main story |
| What technology, model, or cloud would this require? | Tuan; Payod | Slide 1 | I intentionally kept the concept platform-agnostic. The implementation should align with Costco's approved standards, partners, and operating model. | "What approved patterns would the team want this to fit?" | Main story |
| Would this replace existing pharmacy systems? | Brian; Tuan | Slide 1 | No. The concept is intended to complement existing workflows and improve the journey into and across them. | "Which current workflow would remain the destination?" | Main story |
| What happens when the experience is wrong or unavailable? | Brian; Payod | Slide 4 | The experience should have graceful fallback, communicate uncertainty, preserve progress when possible, and hand off with useful context. | "What fallback path must always remain available?" | Main story |
| How is member and pharmacy data protected? | Payod; Tuan | Slide 4 | Through least-privilege access, approved data sources, authentication, consent where required, encryption, auditability, retention controls, and clear scenario boundaries. | "Which data boundaries are already fixed today?" | Main story |
| How does the member remain in control? | Brian; Payod | Slide 4 | The member should see, review, and confirm important actions, with visible defaults, clear explanations, and the ability to stop or change course. | "Where should confirmation be required?" | Main story |
| Where is pharmacist or staff judgment required? | Brian | Slide 4 | Anywhere judgment, safety, or nuance matters, the experience should route to the right person and keep pharmacy staff authoritative. | "Which situations most often need a human decision today?" | Main story |
| How would this be monitored and governed? | Payod; Tuan | Slide 5 | With telemetry, evaluation, auditability, escalation, and ongoing operational ownership so the experience can be monitored and adjusted responsibly. | "What monitoring signal would matter first?" | Main story |
| How would success be measured? | Evan | Slide 5 | By the selected phase and outcome: completion, effort, trust, handoff quality, operational burden, and other measures tied to the agreed North Star. | "Which metric should be primary for the first test?" | Main story |
| What would the first pilot look like? | Evan; Brian | Slide 5 | A bounded scenario with a limited audience, clear success criteria, and explicit stop or change criteria before any scale-up. | "Which narrow scenario feels safest to learn from first?" | Main story |
| How long would implementation take? | Evan; Tuan | Discussion | I would not give a responsible timeline before understanding the scenario, the systems involved, API readiness, governance, and ownership. | "Which dependency is most likely to set the pace?" | Internal Q&A only |
| What operating responsibilities would need to be assigned? | Tuan; Payod | Discussion | A production experience would need clear responsibility for content, workflow rules, monitoring, escalation, incidents, and change management, aligned to Costco's operating model. | "How are these responsibilities handled across the relevant teams today?" | Internal Q&A only |
| Build versus buy? | Tuan; Evan | Discussion | Separate the experience and operating model from the technology choice, then determine what can be reused, what must be integrated, and what should be procured. | "What capabilities already exist and could be reused?" | Internal Q&A only |
| What happens if the first scenario does not demonstrate value? | Evan | Slide 5 | The model is meant to support advance, iterate, change direction, or stop. A weak result is useful if it produces learning and prevents overinvestment. | "Which evidence would matter before expanding?" | Main story |
| How does integration complexity change from Guide to Assist to Anticipate? | Tuan; Payod | Slide 5 | Guide is the lightest touch, Assist requires deeper authenticated workflow integration, and Anticipate requires signals, consent, monitoring, and stronger governance. | "Which phase would you like mapped against the current systems first?" | Main story |

## Delivery Guidance

- Get to the prototype early.
- Use documentation as support, not as material to read aloud.
- Lead with visible improvement and measurable impact.
- Use technical and strategic terminology only when it compresses or clarifies an idea.
- Invite input from the full group rather than directing the presentation only to Evan.
- Be prepared to skip ahead or change sequence.
- When information is missing, explain the decision framework rather than inventing an answer.
- Ask follow-up questions to clarify systems, ownership, data boundaries, and success criteria.
- Treat the prototype as a hypothesis to pressure-test, not as a completed solution.
- Do not reference private or secondhand observations about any attendee in external materials.

## Responsible ways to respond when information is missing

Use statements such as:

"I would need to understand the current architecture and constraints before giving you a responsible answer."

"I do not want to assume how that workflow is implemented internally."

"The answer would depend on the approved identity, API, security, and operating patterns already in place."

"That is a good question for me to take away. I would want to validate the system owner, data boundaries, and workflow dependencies before proposing a design."

"I can describe the decision framework today, but I would not want to manufacture an implementation estimate without the relevant technical context."

## Assumptions not to make

Do not assume:
- A particular cloud provider
- A particular model provider
- Direct model access to pharmacy systems
- APIs are currently available
- Existing systems must be replaced
- The most advanced phase is required
- All scenarios require authentication
- Proactive outreach is always desirable
- AI should execute clinical or safety-sensitive decisions
- One architecture fits every Costco Pharmacy priority

## Scenario integration worksheet

For each prototype scenario, capture:

### Scenario

Name:

Member need:

Priority supported:

### Experience phase

- Guide
- Assist
- Anticipate

### Integration profile

- Public or authenticated
- Read-only or transactional
- Systems potentially involved
- Data required
- Member confirmation required
- Human handoff required
- Graceful fallback
- Monitoring required

### Key unknowns

- System owner
- API availability
- Data permissions
- Security dependencies
- Operational ownership
- Clinical or regulatory boundaries

### Suggested first experiment

Hypothesis:

Limited audience or prototype:

Measures:

Gate criteria:

Possible decision:
- Advance
- Iterate
- Change direction
- Stop

## Relationship to the storyboard

### Slide 1

Keep the opening focused on member experience and outside-in exploration. Do not introduce architecture or vendor positioning unless specifically asked.

### Slide 5

Use the notes to explain that Crawl, Walk, and Run also represent increasing integration depth and operational responsibility.

### Slide 6

For each prototype scenario, identify the likely integration profile, complexity, and unknowns.

### Appendix or backup discussion

Consider an architecture or integration appendix slide only if it materially improves the discussion. Do not add it to the main presentation by default.

## Follow-up work

Tomorrow:
- Align the document with the selected Slide 6 scenarios
- Add scenario-specific integration profiles
- Refine the most likely questions
- Create concise spoken responses
- Determine whether an appendix architecture slide is needed
- Later convert this into a printable meeting-preparation guide
