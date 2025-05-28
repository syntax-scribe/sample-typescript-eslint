[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ConditionalTypeScope.ts`

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