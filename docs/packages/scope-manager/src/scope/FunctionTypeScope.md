[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionTypeScope.ts`

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
📂 **`packages/scope-manager/src/scope/FunctionTypeScope.ts`**

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

### `FunctionTypeScope`

<details><summary>Class Code</summary>

```ts
export class FunctionTypeScope extends ScopeBase<
  ScopeType.functionType,
  | TSESTree.TSCallSignatureDeclaration
  | TSESTree.TSConstructorType
  | TSESTree.TSConstructSignatureDeclaration
  | TSESTree.TSFunctionType
  | TSESTree.TSMethodSignature,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: FunctionTypeScope['upper'],
    block: FunctionTypeScope['block'],
  ) {
    super(scopeManager, ScopeType.functionType, upperScope, block, false);
  }
}
```
</details>


---