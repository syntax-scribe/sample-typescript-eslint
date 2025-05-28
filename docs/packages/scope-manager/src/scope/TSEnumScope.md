[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSEnumScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

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