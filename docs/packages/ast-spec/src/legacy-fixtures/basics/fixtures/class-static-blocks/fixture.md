[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-static-blocks/fixture.ts`**

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  static count = 0;
  static {
    if (someCondition()) {
      count++;
    }
  }
}
```
</details>


---