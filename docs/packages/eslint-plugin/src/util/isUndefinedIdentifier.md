[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isUndefinedIdentifier.ts`

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
📂 **`packages/eslint-plugin/src/util/isUndefinedIdentifier.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |


---

## Functions

### `isUndefinedIdentifier(i: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
export function isUndefinedIdentifier(i: TSESTree.Node): boolean {
  return i.type === AST_NODE_TYPES.Identifier && i.name === 'undefined';
}
```
</details>

- **Parameters**:
  - `i: TSESTree.Node`
- **Return Type**: `boolean`

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