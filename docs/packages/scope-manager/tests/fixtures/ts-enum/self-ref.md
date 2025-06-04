[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `self-ref.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/ts-enum/self-ref.ts`**

## Enums

### `enum Foo`

<details><summary>Enum Code</summary>

```ts
enum Foo {
  a = 1,
  b = Foo.a,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `a` | `1` |  |
| `b` | `Foo.a` |  |


---