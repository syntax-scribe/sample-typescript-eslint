[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Position.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/Position.ts`**

## Interfaces

### `Position`

<details><summary>Interface Code</summary>

```ts
export interface Position {
  /**
   * Column number on the line (0-indexed)
   */
  column: number;
  /**
   * Line number (1-indexed)
   */
  line: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `column` | `number` | ✗ |  |
| `line` | `number` | ✗ |  |


---