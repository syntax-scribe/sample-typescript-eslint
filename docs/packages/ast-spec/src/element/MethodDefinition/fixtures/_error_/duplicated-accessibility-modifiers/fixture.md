[⬅️ Back to Table of Contents](../../../../../../../../index.md)

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
📂 **`packages/ast-spec/src/element/MethodDefinition/fixtures/_error_/duplicated-accessibility-modifiers/fixture.ts`**

## Functions

### `Foo.bar(): void`

<details><summary>Code</summary>

```ts
public public bar() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `Foo`

<details><summary>Class Code</summary>

```ts
class Foo {
  public public bar() {};
}
```
</details>

#### Methods

##### `bar(): void`

<details><summary>Code</summary>

```ts
public public bar() {}
```
</details>


---