[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `class-deco-with-object-param.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| ✨ Decorators | 1 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/class-deco-with-object-param.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@deco` | `Foo` | class | {
  components: {
    val: true,
  },
} |


---

## Functions

### `deco(param: any): (...param: any) => any`

<details><summary>Code</summary>

```ts
declare function deco(...param: any): (...param: any) => any;
```
</details>

- **Parameters**:
  - `param: any`
- **Return Type**: `(...param: any) => any`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
@deco({
  components: {
    val: true,
  },
})
class Foo {}
```
</details>


---