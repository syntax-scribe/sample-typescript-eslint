[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ConditionalTypeScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/ConditionalTypeScope.ts`**

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

### `ConditionalTypeScope`

<details><summary>Class Code</summary>

```ts
export class ConditionalTypeScope extends ScopeBase<
  ScopeType.conditionalType,
  TSESTree.TSConditionalType,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ConditionalTypeScope['upper'],
    block: ConditionalTypeScope['block'],
  ) {
    super(scopeManager, ScopeType.conditionalType, upperScope, block, false);
  }
}
```
</details>


---