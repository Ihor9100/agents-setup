---

name: codegraph
description: Explore an existing codebase with CodeGraph to understand symbols, references, dependencies, callers, callees, data flow, and blast radius before making or reviewing code changes.

---

# CodeGraph

Use CodeGraph for structural exploration of an existing codebase before making or reviewing changes.

Follow repository instructions, including `AGENTS.md`.

## 1. Use It For

Use CodeGraph when you need to understand:

* callers and callees;
* references and implementations;
* dependencies and dependents;
* data flow between layers;
* architectural relationships;
* blast radius of a change;
* unfamiliar existing code;
* follow-up changes;
* review findings.

Typical cases:

* modify existing behavior;
* fix a bug;
* refactor code;
* change a shared contract;
* understand how a feature flows through the system.

## 2. Do Not Force It

Prefer normal file reading or `rg` for:

* exact text search;
* strings and resource names;
* XML or JSON;
* Gradle configuration;
* manifest entries;
* ProGuard/R8 rules;
* comments;
* small obvious local changes.

CodeGraph complements normal repository search; it does not replace it.

## 3. Verify the Index

Before using CodeGraph, ensure you are in the intended repository or worktree.

If `.codegraph/` exists:

* verify it with `codegraph status`.

Do not assume an index from another Git worktree is valid.

If the index is unavailable, invalid, or CodeGraph fails:

* continue with normal repository search and source inspection;
* report the limitation only when it affects confidence or coverage.

## 4. Exploration Workflow

Before changing structurally relevant code:

1. identify the primary symbol, class, function, interface, module, or feature;
2. inspect the relevant source code;
3. use CodeGraph to explore only useful relationships;
4. determine the smallest affected area;
5. inspect concrete affected files;
6. make the change.

Useful relationships may include:

* callers;
* callees;
* references;
* implementations;
* overrides;
* dependencies;
* repository/use-case/view-model relationships;
* mapper chains;
* event or state propagation;
* navigation entry points.

Do not explore the entire repository without a specific reason.

## 5. Blast Radius

Before changing shared or externally used code, check relevant impact such as:

* callers;
* interface implementations;
* overrides;
* tests;
* state or UI consumers;
* mapping layers;
* persistence or network boundaries;
* cross-module dependencies.

Pay extra attention to:

* shared domain models;
* repository interfaces;
* public APIs;
* navigation contracts;
* common UI components;
* serialization models;
* persistence schemas;
* DI bindings.

Keep the analysis proportional to the change.

## 6. Source Code Is Authoritative

CodeGraph is an exploration aid, not the source of truth.

Always inspect actual source code before making implementation decisions.

If CodeGraph conflicts with the repository state, trust the repository.

## 7. Follow-Up Changes

For follow-up requests:

1. start from the new requested change;
2. identify affected symbols;
3. use CodeGraph only as much as needed;
4. inspect the current implementation;
5. make the smallest scoped change;
6. re-check affected usages when behavior or contracts changed.

Do not restart the full task workflow unless the new request introduces significant scope or architectural ambiguity.

## 8. Review Findings

When checking a review finding:

1. inspect the reported code;
2. verify the finding against the actual implementation;
3. use CodeGraph for callers, dependencies, or data flow when relevant;
4. fix only valid in-scope issues.

Do not blindly trust reviewer findings.

## 9. Scope

Avoid:

* unrelated architecture audits;
* opportunistic refactors;
* investigating distant code with no realistic impact;
* changing unrelated issues found during exploration.

Report important out-of-scope issues separately.

## 10. Result

After exploration, understand:

* the relevant entry point;
* important dependencies;
* affected callers or consumers;
* likely blast radius;
* existing implementation pattern;
* concrete files that need inspection or modification.

Do not produce a separate CodeGraph report unless the user asks for one.

Use the findings directly for implementation, review, or investigation.
