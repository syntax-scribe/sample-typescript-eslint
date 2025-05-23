[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSModuleScope.ts`

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
📂 **`packages/scope-manager/src/scope/TSModuleScope.ts`**

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

### `TSModuleScope`

<details><summary>Class Code</summary>

```ts
export class TSModuleScope extends ScopeBase<
  ScopeType.tsModule,
  TSESTree.TSModuleDeclaration,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: TSModuleScope['upper'],
    block: TSModuleScope['block'],
  ) {
    super(scopeManager, ScopeType.tsModule, upperScope, block, false);
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