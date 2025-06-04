[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| ✨ Decorators | 2 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/property-decorators/fixtures/property-decorator-static-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@baz` | `C.a` | property | *none* |
| `@qux` | `C.b` | property | *none* |


---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C {
  @baz static a;
  @qux
  static b;
}
```
</details>


---