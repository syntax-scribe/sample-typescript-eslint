[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-public-parameter-properties/fixture.ts`**

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  constructor(
    public firstName: string,
    public readonly lastName: string,
    public age: number = 30,
    public readonly student: boolean = false,
  ) {}
}
```
</details>


---