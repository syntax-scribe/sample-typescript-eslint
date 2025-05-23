[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassStaticBlockScope.ts`

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
📂 **`packages/scope-manager/src/scope/ClassStaticBlockScope.ts`**

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

### `ClassStaticBlockScope`

<details><summary>Class Code</summary>

```ts
export class ClassStaticBlockScope extends ScopeBase<
  ScopeType.classStaticBlock,
  TSESTree.StaticBlock,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ClassStaticBlockScope['upper'],
    block: ClassStaticBlockScope['block'],
  ) {
    super(scopeManager, ScopeType.classStaticBlock, upperScope, block, false);
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