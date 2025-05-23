[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ConditionalTypeScope.ts`

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

## 🔧 Functions

> No functions found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---