[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `typeof-in-call-signature.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/typeof-in-call-signature.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `A`

<details><summary>Interface Code</summary>

```ts
interface A {
  <T extends typeof obj>(a: typeof obj, b: T): typeof obj;
  new <T extends typeof obj>(a: typeof obj, b: T): typeof obj;
}
```
</details>


---

## Type Aliases

> No type aliases found in this file.


---