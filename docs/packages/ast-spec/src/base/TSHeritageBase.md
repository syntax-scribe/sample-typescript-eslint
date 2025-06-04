[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSHeritageBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/TSHeritageBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSTypeParameterInstantiation` | `../special/TSTypeParameterInstantiation/spec` |
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


---


---

## Interfaces

### `TSHeritageBase`

<details><summary>Interface Code</summary>

```ts
export interface TSHeritageBase extends BaseNode {
  // TODO(#1852) - this should be restricted to MemberExpression | Identifier
  expression: Expression;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `expression` | `Expression` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---