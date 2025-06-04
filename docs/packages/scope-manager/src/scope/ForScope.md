[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ForScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/ForScope.ts`**

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

### `ForScope`

<details><summary>Class Code</summary>

```ts
export class ForScope extends ScopeBase<
  ScopeType.for,
  TSESTree.ForInStatement | TSESTree.ForOfStatement | TSESTree.ForStatement,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ForScope['upper'],
    block: ForScope['block'],
  ) {
    super(scopeManager, ScopeType.for, upperScope, block, false);
  }
}
```
</details>


---