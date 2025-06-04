[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `decorators.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 1 |
| ✨ Decorators | 3 |

## 📚 Table of Contents

- [Decorators](#decorators)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/decorators.ts`**

## Decorators

| Name | Target | Target Type | Arguments |
|------|--------|-------------|----------|
| `@dec` | `C` | class | *none* |
| `@gec` | `C.field` | property | *none* |
| `@gec` | `C.method` | method | *none* |


---

## Functions

### `dec(target: any): void`

<details><summary>Code</summary>

```ts
function dec(target: any) {}
```
</details>

- **Parameters**:
  - `target: any`
- **Return Type**: `void`
### `gec(): (target: any, propertyKey: string) => void`

<details><summary>Code</summary>

```ts
function gec() {
  return (target: any, propertyKey: string) => {};
}
```
</details>

- **Return Type**: `(target: any, propertyKey: string) => void`
### `C.method(): string`

<details><summary>Code</summary>

```ts
@gec() method(): string {
    return '';
  }
```
</details>

- **Return Type**: `string`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
@dec
class C {
  @gec() field: string;
  @gec() method(): string {
    return '';
  }
}
```
</details>

#### Methods

##### `method(): string`

<details><summary>Code</summary>

```ts
@gec() method(): string {
    return '';
  }
```
</details>


---