[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassScope.ts`

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
📂 **`packages/scope-manager/src/scope/ClassScope.ts`**

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

### `ClassScope`

<details><summary>Class Code</summary>

```ts
export class ClassScope extends ScopeBase<
  ScopeType.class,
  TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ClassScope['upper'],
    block: ClassScope['block'],
  ) {
    super(scopeManager, ScopeType.class, upperScope, block, false);
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