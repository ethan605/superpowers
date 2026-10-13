---
name: surgical-commits
description: Use when deciding whether and how to create Git commits during implementation, review fixes, or delegated work
---

# Surgical Commits

## Core principle

Keep each independently reversible purpose in one commit. Task boundaries do not set commit boundaries. Some tasks need several purpose commits and a later review-fix commit. Implementation, tests, documentation, and supporting fixes for the same purpose belong together. Do not group or split by the word “and”, file type, or file count.

Loading this skill does not grant commit permission. The active workflow sets commit authority, actor, timing, and required tests. Follow repository commit-message conventions. Use actual identifiers such as `Task 7` when useful. Do not invent phase identifiers.

## Procedure

1. Read the active workflow. Make sure that it defines task boundaries, purpose, starting state, commit authority, actor, timing, and required tests. Controllers give implementing workers the purpose, task boundaries, starting state, commit authority, and test requirements. Controllers do not silently commit for their workers.
2. Inspect the complete Git state: `HEAD`, staged and unstaged diffs, and untracked paths and contents. Make sure that you know who owns each change before you change the index. If unrelated work is staged, stop and ask without changing that Git state. If ownership or isolation is uncertain, stop and ask without changing that Git state. Keep an authorized staged change for the same purpose staged for its commit.
3. Keep each independently reversible purpose together. Stage only content owned by that purpose. Preserve authorized same-purpose staged content. For a mixed file, isolate only the owned hunks when safe. Otherwise, stop and ask. Do not unstage someone else's work. Do not use an alternate index or path-limited commit to bypass unrelated staged content. Do not discard untracked files.
4. Make sure that the complete staged diff contains the intended purpose before committing. A filename list is not a diff review.
5. Run the required tests before committing. Run the workflow's required initial full suite before the first commit. For later fixes, run their covering tests and any full suite the workflow requires. Do not impose a full-suite run on every intermediate commit or waive a required failure.
6. Commit only when the active workflow authorizes this actor at this point. Do not bypass hooks. Review actual hook changes and failures. If a hook changes task content, rerun applicable tests on that content before any safe retry. Never blindly retry or destructively restore hook changes.
7. After committing, inspect the actual patch and history. Make sure that you identify any remaining staged, unstaged, and untracked changes. If a task has multiple commits or review fixes, review the complete recorded `BASE..HEAD` range. Do not review only the last commit.

## Delegated work

A controller gives each worker the relevant policy, starting state, task boundaries, commit authority, and test requirements. A worker commits only its own authorized purpose. Batched dispatch does not merge unrelated purposes, and the controller does not take over a worker's commits.
