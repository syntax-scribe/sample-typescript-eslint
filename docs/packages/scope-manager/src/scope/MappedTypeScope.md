[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `MappedTypeScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/MappedTypeScope.ts`**

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

### `MappedTypeScope`

<details><summary>Class Code</summary>

```ts
export class MappedTypeScope extends ScopeBase<
  ScopeType.mappedType,
  TSESTree.TSMappedType,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: MappedTypeScope['upper'],
    block: MappedTypeScope['block'],
  ) {
    super(scopeManager, ScopeType.mappedType, upperScope, block, false);
  }
}
```
</details>


---