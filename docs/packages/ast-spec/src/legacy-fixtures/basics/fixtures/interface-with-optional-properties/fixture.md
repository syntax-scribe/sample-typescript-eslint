[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/interface-with-optional-properties/fixture.ts`**

## Interfaces

### `test`

<details><summary>Interface Code</summary>

```ts
interface test {
  foo?;
  bar?: string;
  baz?(foo, bar?: string, baz?);
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `foo` | `any` | ✓ |  |
| `bar` | `string` | ✓ |  |


---