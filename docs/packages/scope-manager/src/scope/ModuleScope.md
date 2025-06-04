[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ModuleScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/ModuleScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ScopeManager` | `../ScopeManager` |
| `Scope` | `./Scope` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Classes

### `ModuleScope`

<details><summary>Class Code</summary>

```ts
export class ModuleScope extends ScopeBase<
  ScopeType.module,
  TSESTree.Program,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ModuleScope['upper'],
    block: ModuleScope['block'],
  ) {
    super(scopeManager, ScopeType.module, upperScope, block, false);
  }
}
```
</details>


---