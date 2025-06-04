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
📂 **`packages/ast-spec/src/legacy-fixtures/property-decorators/fixtures/property-decorator-factory-instance-member/fixture.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@Input` | `SomeComponent.data` | property | *none* |
| `@Output` | `SomeComponent.click` | property | *none* |


---

## Classes

### `SomeComponent`

<details><summary>Class Code</summary>

```ts
class SomeComponent {
  @Input() data;
  @Output()
  click = new EventEmitter();
}
```
</details>


---