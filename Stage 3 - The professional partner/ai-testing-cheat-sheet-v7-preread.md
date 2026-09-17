# AI for Test Strategy & Engineering
## Before You Start

*Read this once. It will save you from the most common mistakes people make when using AI for the first time.*

---

### AI is a smart, fast, and confidently wrong assistant.

It produces beautifully structured, well-worded answers — even when those answers are completely made up. That is not a bug you can spot by how good the output looks. A clean table, a valid JSON block, and a perfectly formatted test case can all be factually wrong.

Your job is not to check whether the AI's output *looks* right. Your job is to check whether it *is* right.

**Three things to always remember:**

**You are the Quality Gate.** Your knowledge of the system, the business, and the requirements is the final check — not the AI. It does not know your product. You do.

**Clean format is not correct logic.** Neatly formatted output does not mean accurate output. Always validate the *content* against your specification, your live system, or a domain expert.

**Treat AI output as a hypothesis, not a fact.** Use it as a starting point to investigate — not as a finished answer to act on.

---

### 🚨 The False-Green Trap

> **A passing test built on a wrong expected value is worse than a failing test.**

It creates the illusion of test coverage that does not actually exist.

**Never copy expected values directly from an AI response into a test.** Always confirm them against a real source: your specification, the live system, or a human expert. A test turning green only proves the test ran — it does not prove the AI was right.

---

### 🛡 What Is an "Ignorance Clause"?

Several prompts in this guide include a `CRITICAL SAFETY RULES` block. The most important rule inside it is the **Ignorance Clause**.

**In plain English:** it instructs the AI — *"If the answer is not in what I gave you, say so. Do not invent it."*

Without this instruction, AI will fill gaps in your documentation with plausible-sounding fiction. With it, you get an honest flag instead.

**When you see `INSUFFICIENT CONTEXT` in the AI's response — stop.** That is the safety net doing its job. Do not rephrase and retry. Go find the missing information first, then come back.

---

*These prompts are practitioner heuristics. They are starting points, not guaranteed outputs. Effectiveness depends on the quality and completeness of the context you provide.*

---

**You're ready. Turn to the cheat sheet and start with Section 1.**
