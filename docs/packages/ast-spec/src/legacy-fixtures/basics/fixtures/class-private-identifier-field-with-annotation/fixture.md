[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-private-identifier-field-with-annotation/fixture.ts`**

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  #priv1: number;
  #priv2: number = 1;

  constructor() {
    this.#priv1 = 1;
  }
}
```
</details>


---