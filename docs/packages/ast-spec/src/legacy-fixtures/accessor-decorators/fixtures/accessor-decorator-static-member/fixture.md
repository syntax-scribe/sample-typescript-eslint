[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/accessor-decorators/fixtures/accessor-decorator-static-member/fixture.ts`**

## Classes

### `User`

<details><summary>Class Code</summary>

```ts
class User {
  @adminonly
  static set y(a) {
    this._y = a;
  }
}
```
</details>


---