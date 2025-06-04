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
📂 **`packages/ast-spec/src/legacy-fixtures/property-decorators/fixtures/property-decorator-factory-static-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@configurable` | `A.prop1` | property | true |
| `@configurable` | `A.prop2` | property | false |


---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  @configurable(true) static prop1;

  @configurable(false)
  static prop2;
}
```
</details>


---