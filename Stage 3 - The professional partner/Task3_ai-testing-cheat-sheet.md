# AI for Software Testing — Prompt Cheat Sheet
**Heuristics, not standards. Verify everything.**

---

## ⚠ Read This First

AI output looks structured and confident regardless of accuracy.
Your domain knowledge is the quality gate — not the AI.
Every output is unverified until you check it.
Structured formatting does not change this.

---

## Never Trust Without Independent Verification

These are the highest-risk areas where AI fails most often:

| Area | Why it's high risk |
|------|--------------------|
| **Expected values in assertions** | Most dangerous failure mode — a wrong value can pass silently (false green) |
| **Boundary conditions** | AI guesses at edges: date arithmetic, floats, off-by-one |
| **Domain / business rules** | Stated confidently, often wrong without your actual spec |
| **Summaries of your system** | Hallucinated features, flows, and constraints are common |
| **Security & compliance assertions** | Never delegate these to AI judgment |
| **Structured output (JSON, Gherkin, tables)** | Looks authoritative — always interrogate the content, not the format |

---

## The False-Green Trap

> **A passing test with a wrong expected value is worse than a failing test.**

It creates false confidence in coverage that doesn't exist.
Always validate expected values against a real oracle — the spec, the system, or a human expert.
Not just against the test running green.

---

## Universal Caveat

> AI may generate plausible-sounding flaws, constraints, or values that do not exist.
> The output of any technique below is a **hypothesis for you to investigate** — not a finding to act on directly.

---

## Techniques — Start Here (Essential 5)

*New to AI-assisted testing? Use only these at first.*

---

### 1. Ground the AI in Your Actual System
**Use for:** Reducing hallucination about your specific codebase or requirements

**Why it works:** The single most effective thing you can do. AI performs dramatically better — and hallucinates far less — when given the real code or spec rather than a description of it.

**Prompt:**
```
Here is the specific function / requirement under test: [paste it].
Based only on this, identify boundary conditions and equivalence classes I should test.
Do not invent details not present in the material I've given you.
```

**Watch out:** Paste the relevant section, not the entire codebase. More context is not always better if it dilutes the relevant signal.

---

### 2. Chain-of-Thought Scratchpad
**Use for:** Complex logic, calculations, multi-step flows

**Why it works:** Forces reasoning before answering. Exposes logical leaps. The scratchpad is often more useful than the final answer — it shows where the model is guessing.

**Prompt:**
```
Before answering, write your step-by-step reasoning in a section labelled [Thinking].
Then give your final answer.
Do not skip this even if the answer seems obvious.
```

**Watch out:** If the scratchpad is thin or skips steps, the answer is unreliable — regardless of how confident the conclusion sounds.

---

### 3. Explicit Uncertainty Elicitation
**Use for:** Before trusting any assertion or expected value

**Why it works:** Without this, AI fills knowledge gaps with plausible-sounding content. This prompt surfaces what the model doesn't actually know.

**Prompt:**
```
For each part of this response, tell me:
(a) what you are uncertain about, and
(b) what I would need to verify independently.
Do not skip parts where you feel confident.
```

**Watch out:** Self-reported uncertainty is a starting point, not a quality certificate. Treat it as a checklist for your own review.

---

### 4. Risk-First Test Idea Generation
**Use for:** Generating meaningful tests anchored in what could go wrong

**Why it works:** Anchors test ideas in risk rather than coverage metrics. Produces more useful results than "generate test cases for this feature."

**Prompt:**
```
List the risks associated with this feature or change.
For each risk, generate test ideas that would expose it.
Prioritise by severity, not likelihood.
```

**Watch out:** Generic risk lists appear when no context is provided. Always paste the actual feature or requirement — vague input produces vague risks.

---

### 5. Adversarial Self-Review
**Use for:** Catching gaps in AI-generated output before you act on it

**Why it works:** Breaks the AI's tendency to validate whatever you show it. More useful than asking "is this good?" — which almost always gets a yes.

**Prompt:**
```
Review your answer as a skeptical senior QA engineer.
List the most significant structural flaws — gaps that would allow a bug to slip through.
Focus on logic and coverage, not wording.
```

**Watch out:** Watch for superficial critique (minor edge cases, style nits). If it only finds small issues, probe further: "What about [specific scenario]?"

---

## Techniques — Advanced

*Use these once you're comfortable with the essential 5.*

---

### 6. Test Oracle Simulation
**Use for:** Describing behaviour without asserting specific expected values

**Why it works:** Separates behaviour description from specific expected values. Reduces the risk of the false-green trap by not asking the AI to assert values it can't reliably derive.

**Prompt:**
```
Explain what the system should do in this scenario, including assumptions.
Do not give exact expected values unless they can be logically derived from the material I've provided.
```

**Watch out:** Challenge any numeric or specific outputs — ask "How did you derive that?"

---

### 7. Ambiguity Finder
**Use for:** Requirement reviews, early in a project

**Why it works:** AI is strong at spotting linguistic ambiguity and underspecification — useful before testing begins.

**Prompt:**
```
List all ambiguous, underspecified, or contradictory parts of this requirement.
Explain why each is ambiguous and what questions a tester should ask to resolve it.
```

**Watch out:** Some flagged ambiguities may not be real. Treat the list as a prompt for discussion, not a definitive finding.

---

### 8. Boundary Expansion
**Use for:** Finding edge cases beyond happy paths

**Why it works:** AI defaults to typical cases. This forces atypical, pathological, and structurally extreme inputs that are easy to miss in manual test design.

**Prompt:**
```
List boundary, extreme, and pathological cases for this requirement.
Include technically possible but unlikely cases.
Do not invent constraints not in the material I've given you.
```

**Watch out:** AI may invent constraints. Cross-check suggested boundaries against the actual spec.

---

### 9. Dual-Perspective Review
**Use for:** Structured critique of a plan, test approach, or design

**Why it works:** Creates surface tension between viewpoints within a single response. Useful for spotting one-sided analysis.

**Prompt:**
```
Act as two reviewers responding to this:
Reviewer A defends the approach.
Reviewer B critiques it specifically.
Summarise the key disagreements.
```

**Watch out:** This is one model playing two roles — it lacks genuine independent tension. If both reviewers agree easily, ask for stronger critique. Real independent review requires a second human or a different model.

---

### 10. Scenario Stressing
**Use for:** Resilience and failure-mode thinking

**Why it works:** AI can enumerate cascading failure scenarios quickly. Useful for exploratory thinking about system behaviour under abnormal conditions.

**Prompt:**
```
Describe how this flow behaves under: high load, slow dependencies, partial failures,
unexpected inputs, and concurrent access.
For each, describe the failure mode and how it might manifest in testing.
```

**Watch out:** Impact analysis may be exaggerated or speculative. Treat output as a starting checklist, not a risk assessment.

---

### 11. Constraint-Aware Test Data Generation
**Use for:** Valid and invalid data generation at volume

**Why it works:** AI is strong at variation and volume. Useful for generating structured test data with deliberate violations.

**Prompt:**
```
Generate test data that satisfies these constraints: [list].
Then generate data that violates each constraint in a subtle, non-obvious way.
```

**Watch out:** AI often breaks constraints accidentally in the "valid" data set too. Validate all generated data before use.

---

### 12. Compare and Contrast
**Use for:** Inconsistency detection between specs, versions, or implementations

**Why it works:** AI is strong at structural comparison. Useful for regression scope analysis.

**Prompt:**
```
Compare these two descriptions.
List differences, contradictions, and uncertainties.
Mark any item you are not certain about.
Do not invent details.
```

**Watch out:** Ask it to mark uncertain items explicitly — otherwise inferences and facts look identical in the output.

---

### 13. Explain Code or Behaviour
**Use for:** Orientation in unfamiliar code before testing it

**Why it works:** AI summarises structure quickly and can flag potential risks. Useful for onboarding to a codebase.

**Prompt:**
```
Explain what this function does, list potential risks or failure modes, and identify inputs
that might cause unexpected behaviour.
Flag anything you're inferring rather than reading directly from the code.
```

**Watch out:** Always verify explanations against the actual code. AI may describe what code looks like it should do, not what it actually does.

---

## How to Get What You Want

### 1. Name the deliverable
Be explicit about the form of output you need. Vague requests produce vague responses.
```
"Give me test ideas only, no explanation."
"Produce a Gherkin scenario, nothing else."
"Rewrite this requirement."
```

### 2. Block unwanted behaviour
Explicitly excluding something is more reliable than hoping the model avoids it.
```
"Do not summarise."
"Do not invent details."
"Do not give expected values."
```

### 3. Paste real context
AI performs dramatically better with the actual requirement, code, or spec.
Descriptions of your system are far less reliable than the thing itself.
```
"Here is the requirement: [paste]"
"Here is the function: [paste]"
"Here is the constraint list: [paste]"
```

### 4. Ask for uncertainties explicitly
Without this, AI presents inferences and facts with equal confidence.
```
"List all assumptions you made."
"Mark anything you are not certain about."
"What would I need to verify independently?"
```

### 5. Handle prompt drift correctly
If the model has lost track of your constraints mid-conversation:
- **Most reliable fix:** Start a new conversation
- **For minor drift:** Re-state your constraint — "Reminder: we are working within [constraint]. Continue from that baseline."

Note: "Ignore previous instructions" is unreliable and can cause unpredictable behaviour. Avoid it.

### 6. Use structured output carefully
Tables, JSON, and Gherkin look authoritative. Request them when you need the format —
but always interrogate the content separately.
```
"Format as Gherkin. After the scenario, list any assumptions you made about expected values."
```

---

## Quick Reference — Prompts Only

| # | Technique | Prompt (abbreviated) |
|---|-----------|----------------------|
| 1 | Ground in real system | "Here is the code/requirement: [paste]. Based only on this..." |
| 2 | Chain-of-thought | "Write reasoning in [Thinking] before answering." |
| 3 | Uncertainty elicitation | "For each part: (a) what you're uncertain about, (b) what I should verify." |
| 4 | Risk-first test ideas | "List risks. For each, generate test ideas. Prioritise by severity." |
| 5 | Adversarial self-review | "Find the most significant structural flaws in what you just wrote." |
| 6 | Test oracle simulation | "Explain behaviour without giving expected values unless logically derived." |
| 7 | Ambiguity finder | "List ambiguous, underspecified, or contradictory parts of this requirement." |
| 8 | Boundary expansion | "List boundary, extreme, and pathological cases. Do not invent constraints." |
| 9 | Dual-perspective review | "Reviewer A defends. Reviewer B critiques. Summarise disagreements." |
| 10 | Scenario stressing | "Describe behaviour under: high load, slow deps, partial failure, bad inputs." |
| 11 | Test data generation | "Generate valid data. Then generate data that violates each constraint subtly." |
| 12 | Compare and contrast | "List differences, contradictions, and uncertainties. Mark uncertain items." |
| 13 | Explain code | "Explain, list risks, identify edge cases. Flag anything you're inferring." |

---

## Research Basis

These techniques are grounded in published research. Verify citations independently before using in formal materials.

- Wei, J. et al. (2022). *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models.* NeurIPS.
- Madaan, A. et al. (2023). *Self-Refine: Iterative Refinement with Self-Feedback.* NeurIPS.
- Anthropic Prompt Engineering Guide — docs.anthropic.com

---

*These are practitioner heuristics. Effectiveness varies by model, task, and user skill.*
*This cheat sheet is not a substitute for QA expertise or domain knowledge.*
