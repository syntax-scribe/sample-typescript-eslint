[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `NodeOrTokenData.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/NodeOrTokenData.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Range` | `./Range` |
| `SourceLocation` | `./SourceLocation` |


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