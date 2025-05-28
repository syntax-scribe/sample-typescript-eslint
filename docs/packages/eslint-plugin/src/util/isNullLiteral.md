[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isNullLiteral.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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
📂 **`packages/eslint-plugin/src/util/isNullLiteral.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isNullLiteral(i: TSESTree.Node): i is TSESTree.NullLiteral`

<details><summary>Code</summary>

```ts
export function isNullLiteral(i: TSESTree.Node): i is TSESTree.NullLiteral {
  return i.type === AST_NODE_TYPES.Literal && i.value == null;
}
```
</details>

- **Parameters**:
  - `i: TSESTree.Node`
- **Return Type**: `i is TSESTree.NullLiteral`

---