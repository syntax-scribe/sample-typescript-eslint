[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-private-parameter-properties/fixture.ts`**

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  constructor(
    private firstName: string,
    private readonly lastName: string,
    private age: number = 30,
    private readonly student: boolean = false,
  ) {}
}
```
</details>


---