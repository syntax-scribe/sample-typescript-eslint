[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 🔄 Re-exports | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/variable/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintScopeVariable` | `./ESLintScopeVariable` |
| `Variable` | `./Variable` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `./ESLintScopeVariable` | ESLintScopeVariable |
| named | `./ImplicitLibVariable` | ImplicitLibVariable, ImplicitLibVariableOptions, LibDefinition |
| named | `./Variable` | Variable |


---

## Type Aliases

### `ScopeVariable`

```ts
type ScopeVariable = ESLintScopeVariable | Variable;
```


---