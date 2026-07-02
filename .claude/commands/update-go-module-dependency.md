---
name: update-go-module-dependency
description: Workflow command scaffold for update-go-module-dependency in kubernetes.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /update-go-module-dependency

Use this workflow when working on **update-go-module-dependency** in `kubernetes`.

## Goal

Updates a Go module dependency across the Kubernetes repository, including updating go.mod, go.sum, staging modules, and vendored code.

## Common Files

- `go.mod`
- `go.sum`
- `go.work.sum`
- `staging/src/k8s.io/*/go.mod`
- `staging/src/k8s.io/*/go.sum`
- `hack/tools/*/go.mod`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update root go.mod and go.sum files with the new dependency version.
- Update go.mod and go.sum in all relevant staging/src/k8s.io/* submodules.
- Update go.mod and go.sum in hack/tools or other tool directories if applicable.
- Update vendor/ directory with the new dependency code and vendor/modules.txt.
- Commit all changes together.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.