# AI for Test Strategy & Engineering — Prompt Cheat Sheet
*Heuristics, not standards. Always verify everything.*

---

## SECTION 1 · PROMPTS FOR YOUR TEST STRATEGY
### Use during the workshop — then keep for reference

These prompts are designed to work with the Test Approach or Strategy document you've been drafting. Paste in your own text and let the AI act as a thinking partner and critical reviewer.

---

### Prompt S1 · Context Setting

**Why use this first?** It tells the AI exactly what you're doing and sets strict rules before you start. Without this, you get generic textbook advice instead of feedback on *your* work.

**▶ Copy this prompt**

```
I am drafting a high-level test strategy for senior stakeholders.
Act as an expert test strategy consultant and a critical peer.
Keep your responses succinct, conversational, and direct.

CRITICAL SAFETY RULES:
- Do NOT invent business rules, system metrics, or architectural details.
- Prefix any inference or assumption you make with [ASSUMPTION].
- If my text lacks the context to answer clearly, output "INSUFFICIENT CONTEXT"
  rather than guessing.

Here is my draft strategy or notes so far:
[PASTE YOUR STRATEGY OR NOTES HERE]
```

---

### Prompt S2 · Sharpen the Strategic Intent

**Why use this?** Executives read for business risk, not technical detail. This turns a long draft into a two-sentence mission statement they will actually read and remember.

**▶ Copy this prompt**

```
Review the strategic intent of my draft below.
Help me rewrite it into a concise, 2-sentence summary that clearly communicates
our core testing objective to a senior stakeholder.
Focus the language on engineering confidence, business continuity, and risk mitigation.

CRITICAL SAFETY RULES:
- Do NOT add new system features or unstated business rules.
- If the core objective is missing from my text, output "INSUFFICIENT CONTEXT".

Here is the text:
[PASTE YOUR STRATEGY DRAFT HERE]
```

---

### Prompt S3 · Challenge Your Focus Areas

**Why use this?** Testing teams often try to test everything equally because they're afraid of missing something. This forces honest prioritisation by tying each focus area to a real business consequence.

**▶ Copy this prompt**

```
Review my chosen testing focus areas and their rationales below. Challenge my logic.
Which technical failures or functional areas pose the greatest threat to business
continuity or stakeholder trust?

Help me refine my top 3 focus areas so that the "Why" behind each one is
clearly linked to protecting business value — not just technical preference.

CRITICAL SAFETY RULES:
- Do NOT invent system constraints or technical dependencies.
- Flag all assumptions with [ASSUMPTION].

My focus areas:
[PASTE YOUR FOCUS AREAS AND RATIONALE HERE]
```

---

### Prompt S4 · Surface Gaps and Friction Points

**Why use this?** It finds the holes in your plan before a skeptical stakeholder does. Better to discover them yourself in a workshop than during an audit.

**▶ Copy this prompt**

```
Act as a highly skeptical stakeholder reviewing my testing approach.
Identify potential documentation gaps, technical unknowns, or requirement ambiguities
I may have glossed over.
Format your output as a concise "Friction Log."

CRITICAL SAFETY RULES:
- If my text lacks sufficient information to evaluate an area, output "INSUFFICIENT CONTEXT".
- Do NOT fill gaps with assumptions or invented business rules.

Strategy:
[PASTE YOUR STRATEGY OR APPROACH HERE]
```

---

### Prompt S5 · Define Confidence Outcomes

**Why use this?** Test pass rates mean nothing to business leaders. This builds outcome statements that prove stability in language your stakeholders actually care about.

**▶ Copy this prompt**

```
Review the outcomes described in my testing approach below.
Help me define 2-3 explicit "Confidence Outcomes" — clear, observable signals that
prove to stakeholders the platform is stable, secure, and ready to scale.
Shift the language away from generic metrics like test pass rates and toward
demonstrable business risk reduction.

CRITICAL SAFETY RULES:
- Do NOT invent metrics, system capabilities, or platform behaviours.
- Flag any assumptions with [ASSUMPTION].

Here is the text:
[PASTE YOUR TESTING OUTCOMES OR APPROACH HERE]
```

---

## SECTION 2 · STARTING PROMPTS
### Your everyday testing toolbox

These are the prompts to reach for during daily work — requirements analysis, test design, and exploratory testing. They are designed to be safe and practical whether you are new to AI or just new to applying it in a testing context.

---

### Prompt B1 · Ambiguity Finder

**Why use this?** Finding requirement flaws before code is written is the cheapest way to prevent bugs. This prompt treats a requirement like a suspect document and lists everything that could trip a tester up.

**▶ Copy this prompt**

```
Analyse the following requirement.
Identify and list any ambiguous, underspecified, or contradictory statements.
Highlight what information is missing that a tester would need in order to
verify the feature accurately.

CRITICAL SAFETY RULES:
- If the text lacks context to clarify a requirement, output "INSUFFICIENT CONTEXT".
- Do NOT infer, guess, or substitute standard industry assumptions for missing details.

Requirement:
[PASTE YOUR FEATURE REQUIREMENT HERE]
```

---

### Prompt B2 · Test Idea Generator

**Why use this?** This breaks you out of tunnel vision fast. It expands your mental model of a feature and surfaces areas you might not have thought to test on your own.

**▶ Copy this prompt**

```
Provide a concise list of high-level test ideas for the following feature.
Group them by:
  1. Functional correctness
  2. Negative and error paths
  3. Basic security and data integrity

Keep descriptions brief — these are ideas to explore, not finished test cases.

CRITICAL SAFETY RULES:
- Do NOT add or assume business rules that are not explicitly stated in my text.

Feature:
[PASTE YOUR FEATURE DESCRIPTION HERE]
```

---

### Prompt B3 · Boundary Explorer

**Why use this?** Left alone, AI suggests obvious, low-value boundaries ("what if the field is empty?"). This forces it to look at structural limits — the ones that actually cause failures.

**▶ Copy this prompt**

```
Look at this feature description and list the likely technical boundary conditions,
extreme inputs, and potential off-by-one risks.
Focus on data types, limits, state transitions, and environmental constraints.

CRITICAL SAFETY RULES:
- Do NOT invent specific numeric limits not implied by the text.
- If a boundary is not defined in the source text, label it clearly as
  "UNDEFINED BOUNDARY — confirm with developer or specification before testing."

Feature:
[PASTE YOUR FEATURE DESCRIPTION HERE]
```

---

### Prompt B4 · Quick Technical Explainer

**Why use this?** Use this when you've been handed an unfamiliar piece of code and need to understand what you're testing before you start testing it.

**▶ Copy this prompt**

```
Explain what this technical component or code snippet does in simple, plain terms.
Highlight the top 3 biggest testing risks or failure modes associated with this logic.
Suggest how a tester could verify each risk without needing to modify the code.

CRITICAL SAFETY RULES:
- Do NOT guess missing behaviours or unstated logic paths.
- If the snippet is too vague to analyse safely, output "INSUFFICIENT CONTEXT".

Component / Code:
[PASTE YOUR CODE OR COMPONENT DESCRIPTION HERE]
```

---

### Prompt B5 · Happy Path Validator

**Why use this?** You must know exactly what a perfect, unobstructed user journey looks like before you can design meaningful edge-case tests. This is your foundation.

**▶ Copy this prompt**

```
Based on this feature specification, outline the absolute minimum end-to-end
user journey required to prove the feature works under optimal conditions.
Define what success looks like at each critical transition point.

CRITICAL SAFETY RULES:
- Do NOT invent user steps, actions, or capabilities not explicitly present in the text.

Specification:
[PASTE YOUR FEATURE SPECIFICATION HERE]
```

---

### Prompt B6 · CRUD Matrix Planner

**Why use this?** Data lifecycle gaps — like what happens to related records when something is deleted — are routinely overlooked during design. This catches them before they become bugs.

**▶ Copy this prompt**

```
For the following data resource or entity, build a simple matrix showing the rules
and expectations for its full data lifecycle: Create, Read, Update, and Delete.
Highlight any missing rules about who can perform each action and under what conditions.

CRITICAL SAFETY RULES:
- If roles, permissions, or lifecycle rules are omitted from the text, do NOT assume
  generic access. Output "CONTEXT OMITTED — confirm with developer or spec" for those fields.

Entity Description:
[PASTE YOUR ENTITY OR DATA RESOURCE DESCRIPTION HERE]
```

---

### Prompt B7 · Persona-Driven Exploratory Charters

**Why use this?** Testing through the eyes of three different user types breaks scripted patterns and surfaces unexpected behaviours that a standard test plan never would.

**▶ Copy this prompt**

```
Generate 3 distinct exploratory testing charters for the feature below,
each based on a different user persona:
  1. A non-technical novice unfamiliar with the system.
  2. An aggressive power user trying to move fast and cut corners.
  3. An administrative auditor focused on data accuracy and access control.

Each charter should include: the persona's goal, their likely behaviours,
and the specific risks their usage pattern creates.

CRITICAL SAFETY RULES:
- Do NOT add system capabilities, permissions, or business rules
  not stated in the feature text.
- If role-based access details are missing, label them "CONTEXT OMITTED".

Feature Description:
[PASTE YOUR FEATURE DESCRIPTION HERE]
```

---

### Prompt B8 · UI Input Validation Checklist

**Why use this?** Front-end field checks are predictable and repeatable. Let the AI draft the checklist so you can spend your time on harder exploratory work.

**▶ Copy this prompt**

```
Generate a checklist of standard input verification tests for the form fields below.
Cover: text length limits, special characters, formatting constraints,
paste behaviour, and empty or null input handling.

CRITICAL SAFETY RULES:
- Do NOT invent validation constraints not stated in the source text.
- If a field's constraints are undefined, label it:
  "VALIDATION RULES UNDEFINED — confirm with developer before writing tests."

Form Fields / UI Description:
[PASTE YOUR FORM DESCRIPTION OR FIELD LIST HERE]
```

---

### Prompt B9 · State Transition Mapper

**Why use this?** Complex systems break most often when someone forces an illegal jump between status states. This maps every valid and invalid path before they cause production incidents.

**▶ Copy this prompt**

```
Analyse the following feature state machine or status lifecycle.
List all valid state transitions.
Point out any hidden paths, unhandled states, or illegal status jumps that a
user or upstream system could accidentally trigger.

CRITICAL SAFETY RULES:
- If the lifecycle rules are incomplete, output "INSUFFICIENT CONTEXT"
  rather than inferring what the missing transitions probably do.

Lifecycle Description:
[PASTE YOUR STATE MACHINE OR LIFECYCLE DESCRIPTION HERE]
```

---

### Prompt B10 · Smoke Test Prioritiser

**Why use this?** A post-deployment smoke suite should be fast and ruthlessly focused. This cuts a sprawling list down to the five checks that matter most immediately after a release.

**▶ Copy this prompt**

```
Review the following list of test ideas or scenarios.
Select the top 5 highest-priority tests to run immediately after a deployment
to quickly confirm system health.
Provide a 1-sentence business justification for why each was chosen.

CRITICAL SAFETY RULES:
- Focus only on the text provided. Do NOT invent new features or test scenarios.

Test List:
[PASTE YOUR FULL TEST LIST HERE]
```

---

## SECTION 3 · ADVANCED PROMPTS
### Higher-leverage tools — use when you have richer context to provide

> **A note before you use these:** These prompts involve deeper architectural and adversarial reasoning. They work best when you can provide detailed architecture notes, incident histories, or schema definitions. If the AI outputs `INSUFFICIENT CONTEXT` or `[UNKNOWN BEHAVIOR]` — that is the safety net working. Resolve the gap before continuing.

---

### Prompt A1 · Scenario Stressing

**Why use this?** Features that work perfectly on a developer's clean local machine often collapse immediately in chaotic production environments. This tests the gap between those two realities.

**▶ Copy this prompt**

```
Analyse this feature or process flow.
Describe how it might fail, degrade, or leak data under each of the following
operational stresses:
  - High concurrency or sustained load
  - Slow or timing-out third-party dependencies
  - Partial or intermittent network failures
  - Malformed or unexpected data payloads

CRITICAL SAFETY RULES:
- Keep all failure modes grounded in the architecture I provide.
- Flag speculative impacts with [ASSUMPTION — not stated in architecture].
- If recovery behaviour is not documented, label it
  [UNKNOWN RECOVERY BEHAVIOUR — verify in code or runbook].

Feature / Flow:
[PASTE YOUR FEATURE DESCRIPTION OR ARCHITECTURE NOTES HERE]
```

---

### Prompt A2 · Dual-Perspective Critique

**Why use this?** AI naturally agrees with whatever you show it. This forces it to break that pattern by simulating a structured debate — one reviewer defends your approach, one attacks it.

**▶ Copy this prompt**

```
Simulate a debate between two expert QA engineers reviewing my testing approach below.

Reviewer A defends the current approach and points out its genuine strengths.
Reviewer B critically attacks it, looking for gaps, weak assumptions,
and overlooked risks.

After the debate, provide:
  - A summary of their core disagreements.
  - A numbered list of actionable changes to harden the approach.

CRITICAL SAFETY RULES:
- Do NOT invent system behaviours, architectural constraints, or testing gaps
  not present in the text I provide.
- If the approach lacks sufficient detail to critique a specific area safely,
  label it "INSUFFICIENT CONTEXT" rather than speculating.

My Approach:
[PASTE YOUR TESTING APPROACH HERE]
```

---

### Prompt A3 · Data Mutation & Constraint Violation

**Why use this?** Ensures validation logic lives in the back-end where it belongs and cannot be bypassed by a clever user or a corrupt payload from an upstream system.

**▶ Copy this prompt**

```
Review the following business rules and data schemas.

First, list 3 examples of perfectly valid data combinations the system should accept.

Second, generate a list of creative, subtle ways a user or upstream system could
violate these constraints — for example: schema poisoning, state-machine bypassing,
logical contradictions, or type confusion — that the system's validation must catch.

CRITICAL SAFETY RULES:
- If schema constraints are missing from my text, output "INSUFFICIENT CONTEXT".
  Do NOT invent standard data types or assume common defaults.

Rules / Schema:
[PASTE YOUR BUSINESS RULES AND DATA SCHEMA HERE]
```

---

### Prompt A4 · Test Consistency Auditor

**Why use this?** AI is unreliable at raw arithmetic but excellent at spotting logical contradictions. This prompt plays to that strength — and explicitly blocks the weakness that causes the False-Green Trap.

**▶ Copy this prompt**

```
Act as a critical consistency auditor for the following system logic.
Evaluate the state changes and system behaviours for the scenarios I provide.

CRITICAL SAFETY RULES:
- Do NOT calculate exact numeric outputs, timestamps, or mock data values.
  (AI is unreliable at precise calculations — this is how the False-Green Trap happens.)
- Map only the logical state transitions.
- Explicitly flag any paths where the logic permits an ambiguous, conflicting,
  or unhandled system state.

System Logic:
[PASTE YOUR SYSTEM LOGIC OR SCENARIO DESCRIPTIONS HERE]
```

---

### Prompt A5 · Dependency Failure Analysis

**Why use this?** Modern systems break most catastrophically at the boundaries between services. This maps what breaks across the system when something downstream goes dark — and flags anywhere the recovery behaviour is undocumented.

**▶ Copy this prompt**

```
Map out what breaks across this feature and its connected systems if upstream or
downstream integrations fail.

Analyse what happens if a connected service responds with each of the following:
  - HTTP 500 (internal server error)
  - HTTP 401 (unauthorised)
  - An empty payload
  - A 30-second timeout

CRITICAL SAFETY RULES:
- Do NOT infer system recovery behaviours if they are not documented in my text.
- Label any undocumented recovery behaviour as:
  [UNKNOWN FAILURE BEHAVIOUR — verify in code, runbook, or architecture docs].

Architecture / Dependency Notes:
[PASTE YOUR ARCHITECTURE OR DEPENDENCY DETAILS HERE]
```

---

### Prompt A6 · Heuristic Testing Framework (SFDPO / RCRCRC)

**Why use this?** Structuring exploratory sessions around proven mnemonics guarantees you don't miss entire risk categories through habit or tunnel vision.

*SFDPO = Structure, Function, Data, Platform, Operations. RCRCRC = Recent, Core, Risk, Configuration, Repair, Chronic. You don't need to memorise them — just paste your specification.*

**▶ Copy this prompt**

```
Apply the SFDPO testing heuristic (Structure, Function, Data, Platform, Operations)
OR the RCRCRC heuristic (Recent, Core, Risk, Configuration, Repair, Chronic)
to the following feature specification.

Generate advanced exploratory test charters with a heavy focus on the
Platform and Operational dimensions — the areas most commonly under-tested.

CRITICAL SAFETY RULES:
- If the specification lacks sufficient detail to generate meaningful charters
  for a dimension, label that dimension "INSUFFICIENT CONTEXT" rather than
  inventing platform or operational assumptions.

Specification:
[PASTE YOUR FEATURE SPECIFICATION HERE]
```

---

### Prompt A7 · Race Condition & Concurrency Hunter

**Why use this?** Timing and collision bugs are nearly invisible during standard testing. They only appear when two things happen at exactly the same moment — this maps those windows before they hit production.

**▶ Copy this prompt**

```
Analyse this multi-step transactional workflow for potential race conditions,
locking problems, or concurrency vulnerabilities.

Identify specific windows where two identical requests sent simultaneously could
cause: duplicate processing, negative balances, or data corruption.

CRITICAL SAFETY RULES:
- Do NOT invent locking mechanisms, retry logic, or queue behaviours
  not described in my workflow.
- If concurrency controls are undocumented, label them:
  [UNKNOWN CONCURRENCY BEHAVIOUR — verify in code before writing tests].

Workflow Description:
[PASTE YOUR WORKFLOW OR TRANSACTION DESCRIPTION HERE]
```

---

### Prompt A8 · Historical Defect Pattern Matcher

**Why use this?** Engineering teams repeat past mistakes when building new features with similar architectural patterns. This connects your incident history to your new build — before the bug repeats itself.

**▶ Copy this prompt**

```
Review this new technical feature description against the summary of our historical
production incidents below.

Identify where the new work shares architectural patterns, dependencies, or
complexity traps with our past bugs.
Suggest 3 highly targeted regression scenarios based on those shared patterns.

CRITICAL SAFETY RULES:
- If the incident history lacks sufficient detail to match patterns safely, output
  "INSUFFICIENT HISTORICAL CONTEXT" rather than speculating about root causes.

New Feature:
[PASTE YOUR NEW FEATURE DESCRIPTION HERE]

Past Incidents:
[PASTE YOUR INCIDENT SUMMARIES OR POST-MORTEM NOTES HERE]
```

---

### Prompt A9 · Asymmetric Input & Security Edge Case Generator

**Why use this?** Standard firewalls are tuned for known attacks. Deep data parsing flaws — hidden control characters, unexpected encodings, type confusion — routinely bypass them. This generates the test data to catch those issues safely.

**▶ Copy this prompt**

```
Review this API endpoint or data intake interface.
Generate a list of non-standard, asymmetric payloads designed to test deep
parsing vulnerabilities, such as:
  - Hidden control characters or null bytes
  - Nested arrays or objects exceeding typical depth limits
  - Type confusion (e.g. sending a string where an integer is expected)
  - Unexpected or mixed character encodings

CRITICAL SAFETY RULES:
- Do NOT generate runnable exploit scripts or code injection payloads.
  Focus strictly on data structure and encoding variation for test input design.

Interface / Endpoint Spec:
[PASTE YOUR API SPECIFICATION OR ENDPOINT DESCRIPTION HERE]
```

---

### Prompt A10 · Error Handling & Recovery Auditor

**Why use this?** Unhandled errors cause three cascading problems: the system enters a broken state, tracking data is lost, and internal error details get leaked to end users. This audits for all three.

**▶ Copy this prompt**

```
Audit this system logic from an error-recovery perspective.
Identify paths where a failure could leave the system in an inconsistent or
partially committed state.

Suggest test scenarios to confirm that errors are:
  1. Correctly caught and handled — no silent failures
  2. Logged with operational tracing identifiers for debugging
  3. Returned to users with secure, non-leaking messages
     (no stack traces, internal IDs, or infrastructure details exposed to users)

CRITICAL SAFETY RULES:
- Do NOT assume standard error-handling patterns exist if not described in my text.
- If error handling or logging behaviour is undocumented, label it:
  [UNKNOWN ERROR BEHAVIOUR — verify in code before writing recovery tests].

System Logic:
[PASTE YOUR SYSTEM LOGIC OR COMPONENT DESCRIPTION HERE]
```

---

*These are practitioner heuristics. Effectiveness varies by model, context window, and the quality of what you paste in. The more specific your context, the more useful the output.*
