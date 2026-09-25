---

name: grill-me
description: Stress-test an idea, plan, design, text, or code by identifying weak assumptions, hidden risks, failure modes, and unclear reasoning when the user explicitly asks to be challenged or grilled.

---

# Grill Me

Stress-test the user's work.

The goal is to expose weak assumptions, hidden risks, unclear reasoning, fragile decisions, and realistic failure modes.

Do not provide reassurance for its own sake.

## 1. Style

* Be direct, specific, and constructive.
* Challenge the work, not the user.
* Skip motivational padding and generic disclaimers.
* Prefer concrete evidence and actionable fixes over vague criticism.
* Do not manufacture problems merely to sound critical.
* Briefly acknowledge strong parts only when useful for context.

## 2. Focus

Prioritize the highest-impact weaknesses.

For software or code, challenge:

* correctness;
* hidden assumptions;
* edge cases;
* architecture and coupling;
* concurrency and lifecycle behavior;
* performance;
* security;
* failure handling;
* maintainability;
* test coverage;
* user-visible regressions.

For plans or technical designs, challenge:

* missing constraints;
* sequencing;
* dependencies;
* scalability;
* operational complexity;
* migration risks;
* rollback strategy;
* failure modes.

For writing, challenge:

* unclear claims;
* weak evidence;
* structure;
* credibility;
* tone mismatch;
* ambiguity;
* likely reader misunderstandings.

For general ideas, challenge:

* assumptions;
* incentives;
* feasibility;
* costs;
* trade-offs;
* real-world failure scenarios.

## 3. Do Not Duplicate Other Workflows

Do not automatically:

* clarify the full task;
* create an implementation plan;
* perform a repository-wide investigation;
* review an entire diff;
* modify files.

If the user's request primarily requires task clarification, use `$clarify-task`.

If it primarily requires implementation planning, use `$planner`.

If it requires reviewing implemented Android/Kotlin changes, use `$android-reviewer`.

`grill-me` exists to challenge the reasoning or proposal, not to replace those workflows.

## 4. Missing Context

If context is incomplete, critique only what can reasonably be assessed.

State important assumptions when necessary.

Do not invent missing requirements or pretend certainty.

If a missing fact prevents meaningful critique, identify that gap directly.

## 5. Output

Lead with the most important weakness.

Use only the sections that add value:

### Core Problem

The highest-impact flaw, risk, or unsupported assumption.

### What Could Break

Realistic failure modes, edge cases, or consequences.

### What To Improve

Concrete changes ordered by impact.

### Better Direction

A stronger alternative or revised approach when useful.

Keep the response focused and high-signal.
