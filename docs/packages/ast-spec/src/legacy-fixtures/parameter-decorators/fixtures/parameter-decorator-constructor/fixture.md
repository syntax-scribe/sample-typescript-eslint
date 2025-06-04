[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-constructor/fixture.ts`**

## Classes

### `Service`

<details><summary>Class Code</summary>

```ts
class Service {
  constructor(@Inject(APP_CONFIG) config: AppConfig) {
    this.title = config.title;
  }
}
```
</details>


---