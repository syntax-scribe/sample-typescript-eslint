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
📂 **`packages/ast-spec/src/legacy-fixtures/parameter-decorators/fixtures/parameter-decorator-instance-member/fixture.ts`**

## Functions

### `Greeter.greet(name: string): string`

<details><summary>Code</summary>

```ts
greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `string`

---

## Classes

### `Greeter`

<details><summary>Class Code</summary>

```ts
class Greeter {
  greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
}
```
</details>

#### Methods

##### `greet(name: string): string`

<details><summary>Code</summary>

```ts
greet(@required name: string) {
    return 'Hello ' + name + '!';
  }
```
</details>


---