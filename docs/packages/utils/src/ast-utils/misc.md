[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `misc.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/misc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../ts-estree` |


---

## Functions

### `isTokenOnSameLine(left: TSESTree.Node | TSESTree.Token, right: TSESTree.Node | TSESTree.Token): boolean`

<details><summary>Code</summary>

```ts
export function isTokenOnSameLine(
  left: TSESTree.Node | TSESTree.Token,
  right: TSESTree.Node | TSESTree.Token,
): boolean {
  return left.loc.end.line === right.loc.start.line;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Determines whether two adjacent tokens are on the same line
 */
```

- **Parameters**:
  - `left: TSESTree.Node | TSESTree.Token`
  - `right: TSESTree.Node | TSESTree.Token`
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