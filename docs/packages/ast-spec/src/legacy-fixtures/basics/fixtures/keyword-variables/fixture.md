[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 1
- **Imports**: 31
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/keyword-variables/fixture.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `abstract` | `fake-module` |
| `as` | `fake-module` |
| `asserts` | `fake-module` |
| `any` | `fake-module` |
| `async` | `fake-module` |
| `await` | `fake-module` |
| `boolean` | `fake-module` |
| `constructor` | `fake-module` |
| `declare` | `fake-module` |
| `get` | `fake-module` |
| `infer` | `fake-module` |
| `is` | `fake-module` |
| `keyof` | `fake-module` |
| `module` | `fake-module` |
| `namespace` | `fake-module` |
| `never` | `fake-module` |
| `readonly` | `fake-module` |
| `require` | `fake-module` |
| `number` | `fake-module` |
| `object` | `fake-module` |
| `set` | `fake-module` |
| `string` | `fake-module` |
| `symbol` | `fake-module` |
| `type` | `fake-module` |
| `undefined` | `fake-module` |
| `unique` | `fake-module` |
| `unknown` | `fake-module` |
| `from` | `fake-module` |
| `global` | `fake-module` |
| `bigint` | `fake-module` |
| `of` | `fake-module` |


---

## Functions

### `C.a(): void`

<details><summary>Code</summary>

```ts
static a() {}
```
</details>

- **Return Type**: `void`
### `C.b(): void`

<details><summary>Code</summary>

```ts
private b() {}
```
</details>

- **Return Type**: `void`
### `C.c(): void`

<details><summary>Code</summary>

```ts
public c() {}
```
</details>

- **Return Type**: `void`
### `C.d(): Generator<any, void, unknown>`

<details><summary>Code</summary>

```ts
protected *d() {
    let x = yield;
  }
```
</details>

- **Return Type**: `Generator<any, void, unknown>`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
class C implements X {
  static a() {}
  private b() {}
  public c() {}
  protected *d() {
    let x = yield;
  }
}
```
</details>

#### Methods

##### `a(): void`

<details><summary>Code</summary>

```ts
static a() {}
```
</details>

##### `b(): void`

<details><summary>Code</summary>

```ts
private b() {}
```
</details>

##### `c(): void`

<details><summary>Code</summary>

```ts
public c() {}
```
</details>

##### `d(): Generator<any, void, unknown>`

<details><summary>Code</summary>

```ts
protected *d() {
    let x = yield;
  }
```
</details>


---

## Interfaces

### `X`

<details><summary>Interface Code</summary>

```ts
interface X {}
```
</details>


---

## Type Aliases

> No type aliases found in this file.


---