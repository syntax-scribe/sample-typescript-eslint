[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `interface-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 2 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/interface-type.ts`**

## Interfaces

### `C<T = any>`

<details><summary>Interface Code</summary>

```ts
interface C<T = any> {}
```
</details>

### `R<T extends C>`

<details><summary>Interface Code</summary>

```ts
interface R<T extends C> {
  foo: C;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `foo` | `C` | ✗ |  |


---