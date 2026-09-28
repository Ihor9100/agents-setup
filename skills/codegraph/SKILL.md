---
name: codegraph
description: Use CodeGraph when you need to understand an existing codebase beyond a single file: explore repository structure, trace dependencies and relationships between classes/functions/modules, find callers or usages, follow data/control flow across files, estimate impact of a change, or identify relevant code before planning, implementing, debugging, refactoring, or reviewing a task. Prefer CodeGraph over manual file-by-file searching when repository-wide context or cross-file relationships matter.
---

# CodeGraph

Use CodeGraph to understand relationships inside an existing repository.

Follow repository instructions such as `AGENTS.md`.

## Use when

- exploring an unfamiliar repository or feature
- finding how classes, functions, interfaces, or modules are connected
- tracing callers, usages, dependencies, implementations, or overrides
- following data or control flow across files
- determining the blast radius of a requested change
- gathering context before planning or implementation
- investigating bugs whose cause may span multiple files or modules
- reviewing changes for downstream impact
- handling follow-up changes where existing relationships need to be re-checked

## Do not use when

Prefer normal source inspection or search when:

- the answer is obvious from the currently opened file
- the task is a tiny isolated edit with no meaningful dependencies
- an exact text search with `rg` is sufficient
- searching strings, resource names, XML, JSON, Gradle configuration, manifest entries, comments, or similar text-based content

CodeGraph complements normal repository search; it does not replace it.

## Initialization

Before using CodeGraph, verify that you are in the intended repository or worktree.

If `.codegraph/` exists, verify the index when needed:

```bash
codegraph status
```

If CodeGraph metadata/index is missing, initialize the current repository or worktree:

```bash
codegraph init
```

Do not assume:

- a globally installed CodeGraph means the repository is initialized
- an index created in another Git worktree is valid for the current worktree

If CodeGraph is unavailable, invalid, or fails, continue using normal repository search and source inspection instead of blocking the task.

## Workflow

1. Identify the symbol, feature, module, flow, or behavior that needs investigation.
2. Inspect the relevant source code.
3. Ensure CodeGraph is initialized for the current repository or worktree.
4. Use CodeGraph to inspect only relevant relationships and dependencies.
5. Determine the smallest affected area and likely blast radius.
6. Inspect the concrete affected source files.
7. Use the findings for planning, implementation, debugging, refactoring, or review.
8. Re-check affected usages when shared behavior or contracts change.

Useful relationships may include:

- callers and callees
- references and implementations
- overrides
- dependencies and dependents
- repository / use-case / view-model relationships
- mapper chains
- event or state propagation
- navigation entry points
- cross-module dependencies

## Source of truth

CodeGraph is an exploration aid, not the source of truth.

Always inspect the actual source code before making implementation decisions.

If CodeGraph conflicts with the current repository state, trust the repository.

## Scope

Keep exploration proportional to the task.

Avoid:

- broad repository scans without a concrete purpose
- unrelated architecture audits
- opportunistic refactors
- investigating distant code with no realistic impact
- changing unrelated issues discovered during exploration

Prefer focused queries over broad exploration.

Do not produce a separate CodeGraph report unless the user asks for one. Use the findings directly in the current task.