[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 8
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/this-type-expanded/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `A.method(this: this): number`

<details><summary>Code</summary>

```ts
public method(this: this): number {
    return this.a;
  }
```
</details>

- **Parameters**:
  - `this: this`
- **Return Type**: `number`
### `A.method2(this: A): this`

<details><summary>Code</summary>

```ts
public method2(this: A): this {
    return this.a;
  }
```
</details>

- **Parameters**:
  - `this: A`
- **Return Type**: `this`
### `A.method3(this: this): number`

<details><summary>Code</summary>

```ts
public method3(this: this): number {
    var fn = () => this.a;
    return fn();
  }
```
</details>

- **Parameters**:
  - `this: this`
- **Return Type**: `number`
- **Calls**:
  - `fn`
### `A.method4(this: A): number`

<details><summary>Code</summary>

```ts
public method4(this: A): number {
    var fn = () => this.a;
    return fn();
  }
```
</details>

- **Parameters**:
  - `this: A`
- **Return Type**: `number`
- **Calls**:
  - `fn`
### `A.staticMethod(this: A): number`

<details><summary>Code</summary>

```ts
static staticMethod(this: A): number {
    return this.a;
  }
```
</details>

- **Parameters**:
  - `this: A`
- **Return Type**: `number`
### `A.typeof(this: A): this`

<details><summary>Code</summary>

```ts
static typeof(this: A): this {
    return typeof this;
  }
```
</details>

- **Parameters**:
  - `this: A`
- **Return Type**: `this`
### `fn(): number`

<details><summary>Code</summary>

```ts
() => this.a
```
</details>

- **Return Type**: `number`
### `fn(): any`

<details><summary>Code</summary>

```ts
() => this.a
```
</details>

- **Return Type**: `any`

---

## Classes

### `A`

<details><summary>Class Code</summary>

```ts
class A {
  public a: number;

  public method(this: this): number {
    return this.a;
  }

  public method2(this: A): this {
    return this.a;
  }

  public method3(this: this): number {
    var fn = () => this.a;
    return fn();
  }

  public method4(this: A): number {
    var fn = () => this.a;
    return fn();
  }

  static staticMethod(this: A): number {
    return this.a;
  }

  static typeof(this: A): this {
    return typeof this;
  }
}
```
</details>

#### Methods

##### `method(this: this): number`

<details><summary>Code</summary>

```ts
public method(this: this): number {
    return this.a;
  }
```
</details>

##### `method2(this: A): this`

<details><summary>Code</summary>

```ts
public method2(this: A): this {
    return this.a;
  }
```
</details>

##### `method3(this: this): number`

<details><summary>Code</summary>

```ts
public method3(this: this): number {
    var fn = () => this.a;
    return fn();
  }
```
</details>

##### `method4(this: A): number`

<details><summary>Code</summary>

```ts
public method4(this: A): number {
    var fn = () => this.a;
    return fn();
  }
```
</details>

##### `staticMethod(this: A): number`

<details><summary>Code</summary>

```ts
static staticMethod(this: A): number {
    return this.a;
  }
```
</details>

##### `typeof(this: A): this`

<details><summary>Code</summary>

```ts
static typeof(this: A): this {
    return typeof this;
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