[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `decorators.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 1
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/decorators.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `dec(target: any): void`

<details><summary>Code</summary>

```ts
function dec(target: any) {}
```
</details>

- **Parameters**:
  - `target: any`
- **Return Type**: `void`
### `gec(): (target: any, propertyKey: string) => void`

<details><summary>Code</summary>

```ts
function gec() {
  return (target: any, propertyKey: string) => {};
}
```
</details>

- **Return Type**: `(target: any, propertyKey: string) => void`
### `C.method(): string`

<details><summary>Code</summary>

```ts
@gec() method(): string {
    return '';
  }
```
</details>

- **Return Type**: `string`

---

## Classes

### `C`

<details><summary>Class Code</summary>

```ts
@dec
class C {
  @gec() field: string;
  @gec() method(): string {
    return '';
  }
}
```
</details>

#### Methods

##### `method(): string`

<details><summary>Code</summary>

```ts
@gec() method(): string {
    return '';
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