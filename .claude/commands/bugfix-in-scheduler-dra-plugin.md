---
name: bugfix-in-scheduler-dra-plugin
description: Workflow command scaffold for bugfix-in-scheduler-dra-plugin in kubernetes.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /bugfix-in-scheduler-dra-plugin

Use this workflow when working on **bugfix-in-scheduler-dra-plugin** in `kubernetes`.

## Goal

Implements a bugfix or code cleanup in the scheduler's dynamic resource allocation (DRA) plugins, typically involving a single file change.

## Common Files

- `pkg/scheduler/framework/plugins/dynamicresources/extendeddynamicresources.go`
- `pkg/scheduler/framework/plugins/dynamicresources/nodeallocatabledynamicresources.go`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Identify bug or redundant code in a DRA plugin source file.
- Edit the relevant Go file to fix the bug or remove code.
- Commit the change with a descriptive message.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.