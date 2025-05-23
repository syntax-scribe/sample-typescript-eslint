[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `method-param-default.ts`

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
📂 **`packages/scope-manager/tests/fixtures/class/declaration/method-param-default.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `A.openPort(printerName: any): this`

<details><summary>Code</summary>

```ts
openPort(printerName = this.printerName) {
    this.tscOcx.ActiveXopenport(printerName);

    return this;
  }
```
</details>

- **Parameters**:
  - `printerName: any`
- **Return Type**: `this`
- **Calls**:
  - `this.tscOcx.ActiveXopenport`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  constructor(printName) {
    this.printName = printName;
  }

  openPort(printerName = this.printerName) {
    this.tscOcx.ActiveXopenport(printerName);

    return this;
  }
}
```
</details>

#### Methods

##### `openPort(printerName: any): this`

<details><summary>Code</summary>

```ts
openPort(printerName = this.printerName) {
    this.tscOcx.ActiveXopenport(printerName);

    return this;
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---