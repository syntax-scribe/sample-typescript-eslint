[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `NodeOrTokenData.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/NodeOrTokenData.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Range` | `./Range` |
| `SourceLocation` | `./SourceLocation` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `NodeOrTokenData`

<details><summary>Interface Code</summary>

```ts
export interface NodeOrTokenData {
  type: string;

  /**
   * The source location information of the node.
   *
   * The loc property is defined as nullable by ESTree, but ESLint requires this property.
   */
  loc: SourceLocation;

  range: Range;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `string` | ✗ |  |
| `loc` | `SourceLocation` | ✗ |  |
| `range` | `Range` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---