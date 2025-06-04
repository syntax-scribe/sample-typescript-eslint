[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-static-member/fixture.ts`**

## Functions

### `StaticGreeter.greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `string`

---

## Classes

### `StaticGreeter`

<details><summary>Class Code</summary>

```ts
class StaticGreeter {
  static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
}
```
</details>

#### Methods

##### `greet(name: string): string`

<details><summary>Code</summary>

```ts
static greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>


---