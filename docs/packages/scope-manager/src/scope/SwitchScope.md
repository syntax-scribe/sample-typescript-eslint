[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SwitchScope.ts`

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

## 🔧 Functions

> No functions found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---