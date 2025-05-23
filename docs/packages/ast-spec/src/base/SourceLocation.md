[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SourceLocation.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/SourceLocation.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Position` | `./Position` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---