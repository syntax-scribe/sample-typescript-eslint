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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/private-fields-in-in/fixture.ts`**

## Functions

### `Foo.method(arg: any): boolean`

<details><summary>Code</summary>

```ts
method(arg) {
    return #prop1 in arg;
  }
```
</details>

- **Parameters**:
  - `arg: any`
- **Return Type**: `boolean`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  #prop1;
  method(arg) {
    return #prop1 in arg;
  }
}
```
</details>

#### Methods

##### `method(arg: any): boolean`

<details><summary>Code</summary>

```ts
method(arg) {
    return #prop1 in arg;
  }
```
</details>


---