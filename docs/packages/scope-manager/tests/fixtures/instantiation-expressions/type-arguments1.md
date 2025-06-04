[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-arguments1.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 2 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/instantiation-expressions/type-arguments1.ts`**

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo<T> {
  value: T;
}
```
</details>

### `Bar`

<details><summary>Class Code</summary>

```ts
class Bar<T> {
  foo = Foo<T>;
}
```
</details>


---