[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `class-deco-with-object-param.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/decorators/class-deco-with-object-param.ts`**

## 📦 Imports

> No imports found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---