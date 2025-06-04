[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TypeScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/TypeScope.ts`**

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

### `TypeScope`

<details><summary>Class Code</summary>

```ts
export class TypeScope extends ScopeBase<
  ScopeType.type,
  TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeAliasDeclaration,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: TypeScope['upper'],
    block: TypeScope['block'],
  ) {
    super(scopeManager, ScopeType.type, upperScope, block, false);
  }
}
```
</details>


---