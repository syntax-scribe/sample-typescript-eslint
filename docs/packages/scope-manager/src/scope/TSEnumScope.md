[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSEnumScope.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/TSEnumScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ScopeManager` | `../ScopeManager` |
| `Scope` | `./Scope` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `TSEnumScope`

<details><summary>Class Code</summary>

```ts
export class TSEnumScope extends ScopeBase<
  ScopeType.tsEnum,
  TSESTree.TSEnumDeclaration,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: TSEnumScope['upper'],
    block: TSEnumScope['block'],
  ) {
    super(scopeManager, ScopeType.tsEnum, upperScope, block, false);
  }
}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---