---

name: implement-task
description: Implement a software-development task end-to-end in an isolated worktree using CodeGraph-assisted planning, clarification when needed, implementation, verification, independent review, and optional approved remote delivery.

---

# Implement Task

Implement the requested software-development task end-to-end.

Act as the main orchestrator and implementer.

Follow all applicable repository instructions, including `AGENTS.md`.

## 1. Workspace Setup

Before planning or modifying production code, ensure the task runs in an isolated Git worktree.

Prefer, in order:

1. an existing appropriate Codex-managed worktree;
2. a newly created Codex-managed worktree;
3. an existing isolated Git worktree;
4. a manually created Git worktree as fallback.

Do not modify the user's primary working tree during normal task implementation.

Determine from task and repository context:

* repository;
* project name;
* ticket ID;
* task type;
* base branch;
* short task description.

### Branch Naming

Use:

`<type>/<ticket>-<short-description>`

Supported default types:

* `task`
* `bug`
* `improvement`

Examples:

`task/GT-1020-recipient-loading`

`bug/GT-1042-transfer-state-restoration`

`improvement/GT-1088-contact-sync`

Determine the type from the task tracker or context.

If it cannot be determined reliably, use `task` unless repository conventions indicate otherwise.

### Worktree Naming

Use:

`<project>/<branch-name>`

Examples:

`GTBank/task/GT-1020-recipient-loading`

`GTBank/bug/GT-1042-transfer-state-restoration`

`Chirp/task/CH-231-chat-screen-tests`

The worktree name must contain the complete branch name after the project name.

### Naming Rules

* preserve the official ticket ID;
* derive the description from the task title or primary intent;
* use lowercase kebab-case for the description;
* keep it short and meaningful, preferably 2–5 words;
* remove punctuation and unnecessary words;
* follow explicit repository conventions when they conflict with these defaults.

### Worktree Safety

Before continuing, verify:

* expected repository;
* correct base branch;
* correct task branch;
* correct worktree;
* the agent is actually operating inside that worktree;
* unrelated local changes are not included.

Do not reuse a branch that is already checked out in another worktree.

Use the selected worktree as the working directory for all remaining steps.

Do not copy credentials, secrets, keystores, or sensitive ignored files unless explicitly required and permitted.

For Android projects, ensure required local build configuration such as Android SDK paths is available before verification.

Never commit machine-local configuration such as `local.properties`, credentials, API keys, or keystores.

## 2. CodeGraph Preparation

After selecting or creating the task worktree, prepare CodeGraph for that worktree.

If `.codegraph/` exists:

* verify it with `codegraph status`.

If `.codegraph/` does not exist, but CodeGraph is installed and the repository is intended to use it:

1. run `codegraph init` inside the task worktree;
2. verify it with `codegraph status`.

Never assume or reuse a CodeGraph index from another worktree, because it may represent a different branch or filesystem state.

If CodeGraph is unavailable or initialization fails:

* continue using normal repository search and file-reading tools;
* report the limitation when relevant.

For all subsequent structural codebase exploration, follow the `$codegraph` skill.

## 3. Plan

Before modifying production code, spawn a fresh planning subagent.

Have it use the `$planner` skill to:

* investigate the task and relevant code;
* follow the `$codegraph` skill for structural codebase exploration;
* identify affected areas and existing patterns;
* identify unresolved decisions;
* produce a minimal implementation plan.

The planning subagent must not modify files.

Wait for its result.

## 4. Resolve Ambiguity

Evaluate the plan yourself.

Do not ask questions that can reasonably be answered from the task or repository.

If a material product, UX, backend-contract, compatibility, or architectural decision remains unresolved:

1. stop before implementation;
2. ask concise, grouped questions in the main thread;
3. wait for the user's answer;
4. incorporate it into the requirements and plan.

Never silently guess material decisions.

If no material ambiguity remains, continue without confirmation.

## 5. Implement

Implement the task in the main agent.

Follow:

* agreed requirements;
* planner findings;
* repository instructions;
* existing abstractions and patterns;
* the `$codegraph` skill when structural code exploration is needed.

Keep changes within scope.

Avoid unrelated refactoring or fixes.

Inspect actual source code before making implementation decisions.

If a new material ambiguity appears, ask the user rather than guessing.

## 6. Verify

After implementation:

1. inspect the diff;
2. run the smallest relevant compilation, tests, and checks required by the repository;
3. fix failures caused by the implementation;
4. leave unrelated pre-existing failures unchanged;
5. record anything that could not be verified.

Prefer focused verification over unnecessarily broad checks.

## 7. Independent Review

After verification, spawn a new fresh subagent.

Have it use the `$android-reviewer` skill to independently review the current changes.

The reviewer:

* must not modify files;
* must independently inspect the implementation;
* should follow the `$codegraph` skill when structural codebase exploration is useful;
* should not be told what findings to expect.

Wait for its result.

## 8. Handle Review Findings

Evaluate every finding against the actual code.

For each finding:

* fix it if valid and within scope;
* ignore it if invalid;
* leave unrelated pre-existing issues unchanged;
* ask the user if resolving it requires a new material decision.

Do not blindly trust reviewer findings.

When investigating review findings that involve callers, dependencies, usages, data flow, or architecture, follow the `$codegraph` skill.

## 9. Final Verification

After review fixes:

1. rerun affected checks when needed;
2. inspect the final diff;
3. remove temporary verification files;
4. confirm unrelated changes were not modified;
5. confirm the implementation still matches the agreed requirements.

## 10. Remote Delivery Approval

Do not commit, push, create a PR/MR, assign users, or otherwise modify the remote repository without explicit user approval.

When the task is ready, automatically prepare a complete delivery proposal using repository, Git, task, and available integration context.

Prefill, when reliably determinable:

* source branch;
* remote;
* target/base branch;
* commit message;
* PR/MR title;
* PR/MR description when useful;
* assignee;
* reviewers;
* push: yes/no;
* create PR/MR: yes/no;
* verification status.

Prefer inferred defaults instead of asking the user to fill fields manually.

Use sensible defaults such as:

* source branch: current task branch;
* remote: configured repository remote;
* target branch: normal repository integration branch;
* assignee: current user when known;
* reviewers: repository conventions, CODEOWNERS, task context, or known team configuration;
* commit and PR/MR title: derived from the task ID and implemented change;
* push: yes;
* create PR/MR: yes.

Never invent uncertain identities or repository settings.

Mark unresolved fields clearly.

Present one final proposal, for example:

> Ready for remote delivery:
>
> * Source: `task/GT-1020-recipient-loading`
> * Remote: `origin`
> * Target: `develop`
> * Commit: `GT-1020 Optimize recipient loading`
> * MR title: `GT-1020 Optimize recipient loading`
> * Assignee: Ihor
> * Reviewers: Petro, Oleksii
> * Push: yes
> * Create MR: yes
> * Verification: passed
>
> Approve this delivery plan?

The user should normally only need to approve it or specify exceptions.

Examples:

> Approve.

> Approve, but target `master`.

> Remove Oleksii from reviewers and proceed.

> Push only; do not create the MR.

> Do not deliver remotely.

Only after explicit approval:

1. re-check `git status` and the final diff;
2. ensure unrelated changes are excluded;
3. create the approved commit if required;
4. push the approved branch;
5. create the approved PR/MR;
6. set the approved assignee and reviewers;
7. report the resulting commit SHA, source branch, target branch, PR/MR URL, assignee, reviewers, and available CI status.

Never:

* push directly to the target branch unless explicitly approved;
* force-push unless explicitly approved;
* change approved delivery settings silently;
* merge the PR/MR unless explicitly requested.

## 11. Completion

Report concisely:

* what was implemented;
* important user decisions;
* reviewer result and handled findings;
* tests/checks run;
* CodeGraph status or limitation when relevant;
* anything not verified;
* relevant out-of-scope issues;
* remote delivery result, if performed.
