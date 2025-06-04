[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `UnaryExpressionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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
📂 **`packages/ast-spec/src/base/UnaryExpressionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


---


---

## Interfaces

### `UnaryExpressionBase`

<details><summary>Interface Code</summary>

```ts
export interface UnaryExpressionBase extends BaseNode {
  argument: Expression;
  operator: string;
  prefix: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `argument` | `Expression` | ✗ |  |
| `operator` | `string` | ✗ |  |
| `prefix` | `boolean` | ✗ |  |


---