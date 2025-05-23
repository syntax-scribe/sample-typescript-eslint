[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `parameter-properties.ts`

## 📚 Table of Contents

- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/class/declaration/parameter-properties.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  constructor(
    private a,
    private b = 1,
    private c = a,
    public d = outer,
    public e,
    readonly f: Outer,
  ) {
    a;
  }
}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Outer`

```ts
type Outer = 1;
```


---