---

name: clarify-task
description: Clarify software-development tasks before implementation by identifying unresolved requirements, behavior, scope, edge cases, contracts, and acceptance criteria. Inspect relevant repository context first and ask only questions that cannot reasonably be answered from the codebase.

---

# Clarify Task

Clarify the requested software-development task before implementation.

The goal is to turn an incomplete or ambiguous task into an implementation-ready specification.

Do not modify production code.

Follow all applicable repository instructions, including `AGENTS.md`.

## 1. Inspect Before Asking

Before asking questions:

1. read the task carefully;
2. inspect only repository context relevant to the requested behavior;
3. follow the `$codegraph` skill when structural codebase exploration is needed;
4. inspect actual source code where implementation details matter;
5. answer questions from the repository whenever reasonably possible.

Do not ask the user for information that can be determined from the task or codebase.

## 2. Identify Unknowns

Separate:

* confirmed repository facts;
* requirements explicitly stated by the task or user;
* unresolved product or UX decisions;
* unresolved backend or data-contract decisions;
* compatibility or behavioral constraints;
* assumptions that would otherwise be required.

Do not silently convert material unknowns into assumptions.

## 3. Ask Only Material Questions

Ask concise, grouped questions only when the answers materially affect implementation.

Prioritize ambiguity involving:

* user-visible behavior;
* scope;
* API or data contracts;
* persistence;
* edge cases;
* error handling;
* compatibility;
* architecture;
* acceptance criteria;
* required testing behavior.

Challenge contradictory requirements when necessary.

Do not ask preference questions that do not materially change the implementation.

## 4. Scope Control

Do not automatically expand the task because repository inspection reveals:

* unrelated bugs;
* refactoring opportunities;
* technical debt;
* optional improvements.

Mention them separately only if they materially affect the requested task.

## 5. Completion

When material ambiguities are resolved, return:

### Agreed Requirements

A concise summary of confirmed behavior and constraints.

### Remaining Assumptions

Only assumptions that are low-risk enough to proceed with.

Write `None` if none remain.

### Out of Scope

Relevant items explicitly excluded from the task.

Write `None` if nothing important needs to be called out.

### Unresolved Decisions

Write `None` if the task is implementation-ready.

Otherwise list only the remaining decisions that still require user input.

Do not produce a detailed implementation plan.

Planning belongs to the `$planner` skill.
