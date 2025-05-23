[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassFieldInitializerScope.ts`

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
📂 **`packages/scope-manager/src/scope/ClassFieldInitializerScope.ts`**

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

### `ClassFieldInitializerScope`

<details><summary>Class Code</summary>

```ts
export class ClassFieldInitializerScope extends ScopeBase<
  ScopeType.classFieldInitializer,
  // the value expression itself is the block
  TSESTree.Expression,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ClassFieldInitializerScope['upper'],
    block: ClassFieldInitializerScope['block'],
  ) {
    super(
      scopeManager,
      ScopeType.classFieldInitializer,
      upperScope,
      block,
      false,
    );
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