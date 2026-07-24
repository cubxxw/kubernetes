```markdown
# kubernetes Development Patterns

> Auto-generated skill from repository analysis

## Overview
This skill teaches you how to contribute to the Kubernetes codebase, focusing on Go development conventions, repository structure, and common workflows such as updating dependencies and fixing bugs in scheduler plugins. You'll learn the coding patterns, file organization, and step-by-step processes for maintaining and improving Kubernetes.

## Coding Conventions

### File Naming
- Use **camelCase** for file names.
  - Example: `dynamicResourcePlugin.go`

### Import Style
- Use **relative imports** within the module.
  - Example:
    ```go
    import (
        "context"
        "k8s.io/kubernetes/pkg/scheduler/framework"
    )
    ```

### Export Style
- Use **named exports** for functions, types, and variables.
  - Example:
    ```go
    // Exported function
    func NewDynamicResourcePlugin() *DynamicResourcePlugin {
        // ...
    }
    ```

### Commit Messages
- **Freeform style** (no strict prefix), average length ~58 characters.
  - Example:  
    `Fix resource leak in dynamic resource plugin`

## Workflows

### update-go-module-dependency
**Trigger:** When you need to update a third-party Go dependency across the Kubernetes repository.  
**Command:** `/update-go-dependency`

1. Update the root `go.mod` and `go.sum` files with the new dependency version.
2. Update `go.mod` and `go.sum` in all relevant `staging/src/k8s.io/*` submodules.
3. Update `go.mod` and `go.sum` in `hack/tools` or other tool directories if applicable.
4. Update the `vendor/` directory with the new dependency code and `vendor/modules.txt`.
5. Commit all changes together with a clear message.

**Example:**
```sh
# Update root dependency
go get golang.org/x/net@v0.12.0

# Update staging modules
cd staging/src/k8s.io/apiserver
go get golang.org/x/net@v0.12.0

# Update vendor
go mod vendor

# Commit
git add go.mod go.sum vendor/ staging/src/k8s.io/*/go.mod staging/src/k8s.io/*/go.sum
git commit -m "Update golang.org/x/net to v0.12.0 across repository"
```

**Files Involved:**
- `go.mod`, `go.sum`, `go.work.sum`
- `staging/src/k8s.io/*/go.mod`, `staging/src/k8s.io/*/go.sum`
- `hack/tools/*/go.mod`, `hack/tools/*/go.sum`
- `vendor/**`, `vendor/modules.txt`

---

### bugfix-in-scheduler-dra-plugin
**Trigger:** When you need to fix a bug or remove dead code in the scheduler's dynamic resource allocation (DRA) plugins.  
**Command:** `/fix-dra-plugin-bug`

1. Identify the bug or redundant code in a DRA plugin source file.
2. Edit the relevant Go file to fix the bug or remove the code.
3. Commit the change with a descriptive message.

**Example:**
```go
// Before: Buggy code in extendeddynamicresources.go
if resource == nil {
    return nil
}

// After: Fix nil pointer dereference
if resource == nil {
    return errors.New("resource is nil")
}
```
```sh
git add pkg/scheduler/framework/plugins/dynamicresources/extendeddynamicresources.go
git commit -m "Fix nil pointer dereference in DRA plugin"
```

**Files Involved:**
- `pkg/scheduler/framework/plugins/dynamicresources/extendeddynamicresources.go`
- `pkg/scheduler/framework/plugins/dynamicresources/nodeallocatabledynamicresources.go`

## Testing Patterns

- **Testing framework:** Unknown (likely Go's built-in `testing` package)
- **Test file pattern:** `*.test.*`
  - Example: `dynamicResourcePlugin.test.go`
- **Typical test structure:**
    ```go
    func TestDynamicResourcePlugin(t *testing.T) {
        // Arrange
        // Act
        // Assert
    }
    ```

## Commands
| Command                | Purpose                                                      |
|------------------------|--------------------------------------------------------------|
| /update-go-dependency  | Update a Go module dependency across the repository          |
| /fix-dra-plugin-bug    | Fix a bug or remove dead code in scheduler DRA plugins       |
```
