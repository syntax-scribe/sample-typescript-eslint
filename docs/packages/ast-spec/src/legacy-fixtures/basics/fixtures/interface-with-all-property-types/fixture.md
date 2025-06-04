[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/interface-with-all-property-types/fixture.ts`**

## Interfaces

### `Foo`

<details><summary>Interface Code</summary>

```ts
interface Foo {
  baa: number;
  bar?: number;
  [bax]: string;
  [baz]?: string;
  [eee: number]: string;
  doo(): void;
  coo?(a, b, c): void;
  [loo]?(a, b, c): void;
  boo<J>(a, b, c): void;
  new (a, b?): string;
  new <F>(a, b?): string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `baa` | `number` | ✗ |  |
| `bar` | `number` | ✓ |  |
| `[bax]` | `string` | ✗ |  |
| `[baz]` | `string` | ✓ |  |


---