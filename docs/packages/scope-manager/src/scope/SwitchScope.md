[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SwitchScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/SwitchScope.ts`**

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

### `SwitchScope`

<details><summary>Class Code</summary>

```ts
export class SwitchScope extends ScopeBase<
  ScopeType.switch,
  TSESTree.SwitchStatement,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: SwitchScope['upper'],
    block: SwitchScope['block'],
  ) {
    super(scopeManager, ScopeType.switch, upperScope, block, false);
  }
}
```
</details>


---