[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SourceLocation.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/SourceLocation.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Position` | `./Position` |


---

## Interfaces

### `SourceLocation`

<details><summary>Interface Code</summary>

```ts
export interface SourceLocation {
  /**
   * The position of the first character after the parsed source region
   */
  end: Position;
  /**
   * The position of the first character of the parsed source region
   */
  start: Position;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `end` | `Position` | ✗ |  |
| `start` | `Position` | ✗ |  |


---