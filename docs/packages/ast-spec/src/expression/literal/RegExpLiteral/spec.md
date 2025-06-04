[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/literal/RegExpLiteral/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `LiteralBase` | `../../../base/LiteralBase` |


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