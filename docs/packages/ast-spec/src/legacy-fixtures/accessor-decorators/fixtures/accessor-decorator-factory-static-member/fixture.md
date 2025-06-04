[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/accessor-decorators/fixtures/accessor-decorator-factory-static-member/fixture.ts`**

## Classes

### `Other`

<details><summary>Class Code</summary>

```ts
class Other {
  @foo({ baz: true })
  static get bar() {
    return this._bar;
  }
}
```
</details>


---