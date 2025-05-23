[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isNullLiteral.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---