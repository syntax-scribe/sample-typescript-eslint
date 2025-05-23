[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `spec.ts`

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
📂 **`packages/ast-spec/src/expression/literal/RegExpLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LiteralBase` | `../../../base/LiteralBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `RegExpLiteral`

<details><summary>Interface Code</summary>

```ts
export interface RegExpLiteral extends LiteralBase {
  regex: {
    flags: string;
    pattern: string;
  };
  value: RegExp | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `regex` | `{
    flags: string;
    pattern: string;
  }` | ✗ |  |
| `value` | `RegExp | null` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---