[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 1 |
| 📦 Imports | 31 |
| 📊 Variables & Constants | 32 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `abstract` | `1` | const | `1` | ✗ |
| `as` | `1` | const | `1` | ✗ |
| `asserts` | `1` | const | `1` | ✗ |
| `any` | `1` | const | `1` | ✗ |
| `async` | `1` | const | `1` | ✗ |
| `await` | `1` | const | `1` | ✗ |
| `boolean` | `1` | const | `1` | ✗ |
| `constructor` | `1` | const | `1` | ✗ |
| `declare` | `1` | const | `1` | ✗ |
| `get` | `1` | const | `1` | ✗ |
| `infer` | `1` | const | `1` | ✗ |
| `is` | `1` | const | `1` | ✗ |
| `keyof` | `1` | const | `1` | ✗ |
| `module` | `1` | const | `1` | ✗ |
| `namespace` | `1` | const | `1` | ✗ |
| `never` | `1` | const | `1` | ✗ |
| `readonly` | `1` | const | `1` | ✗ |
| `require` | `1` | const | `1` | ✗ |
| `number` | `1` | const | `1` | ✗ |
| `object` | `1` | const | `1` | ✗ |
| `set` | `1` | const | `1` | ✗ |
| `string` | `1` | const | `1` | ✗ |
| `symbol` | `1` | const | `1` | ✗ |
| `type` | `1` | const | `1` | ✗ |
| `undefined` | `1` | const | `1` | ✗ |
| `unique` | `1` | const | `1` | ✗ |
| `unknown` | `1` | const | `1` | ✗ |
| `from` | `1` | const | `1` | ✗ |
| `global` | `1` | const | `1` | ✗ |
| `bigint` | `1` | const | `1` | ✗ |
| `of` | `1` | const | `1` | ✗ |
| `x` | `any` | let/var | `yield` | ✗ |


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