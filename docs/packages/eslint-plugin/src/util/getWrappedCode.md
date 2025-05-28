[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappedCode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getWrappedCode.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `OperatorPrecedence` | `./getOperatorPrecedence` |


---

## Functions

### `getWrappedCode(text: string, nodePrecedence: OperatorPrecedence, parentPrecedence: OperatorPrecedence): string`

<details><summary>Code</summary>

```ts
export function getWrappedCode(
  text: string,
  nodePrecedence: OperatorPrecedence,
  parentPrecedence: OperatorPrecedence,
): string {
  return nodePrecedence > parentPrecedence ? text : `(${text})`;
}
```
</details>

- **Parameters**:
  - `text: string`
  - `nodePrecedence: OperatorPrecedence`
  - `parentPrecedence: OperatorPrecedence`
- **Return Type**: `string`

---