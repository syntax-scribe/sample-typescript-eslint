[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 🧱 Classes | 1 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/class-with-optional-computed-method/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `computed1` | `"buzz"` | const | `'buzz'` | ✗ |
| `computed2` | `"bazz"` | const | `'bazz'` | ✗ |
| `obj` | `{ member: string; member2: string; }` | const | `{
  member: 'member',
  member2: 'member2',
}` | ✗ |


---

## Functions

### `X.[computed1](): any`

<details><summary>Code</summary>

```ts
[computed1]?();
```
</details>

- **Return Type**: `any`
### `X.[computed2](): void`

<details><summary>Code</summary>

```ts
[computed2]?() {}
```
</details>

- **Return Type**: `void`
### `X.[1](): any`

<details><summary>Code</summary>

```ts
[1]?();
```
</details>

- **Return Type**: `any`
### `X.[2](): void`

<details><summary>Code</summary>

```ts
[2]?() {}
```
</details>

- **Return Type**: `void`
### `X.['literal1'](): any`

<details><summary>Code</summary>

```ts
['literal1']?();
```
</details>

- **Return Type**: `any`
### `X.['literal2'](): void`

<details><summary>Code</summary>

```ts
['literal2']?() {}
```
</details>

- **Return Type**: `void`
### `X.[obj.member](): void`

<details><summary>Code</summary>

```ts
[obj.member]?() {}
```
</details>

- **Return Type**: `void`
### `X.[obj.member2](): any`

<details><summary>Code</summary>

```ts
[obj.member2]?();
```
</details>

- **Return Type**: `any`
### `X.[f()](): void`

<details><summary>Code</summary>

```ts
[f()]?() {}
```
</details>

- **Return Type**: `void`

---

## Classes

### `X`

<details><summary>Class Code</summary>

```ts
class X {
  [computed1]?();
  [computed2]?() {}
  [1]?();
  [2]?() {}
  ['literal1']?();
  ['literal2']?() {}
  [obj.member]?() {}
  [obj.member2]?();
  [f()]?() {}
}
```
</details>

#### Methods

##### `[computed1](): any`

<details><summary>Code</summary>

```ts
[computed1]?();
```
</details>

##### `[computed2](): void`

<details><summary>Code</summary>

```ts
[computed2]?() {}
```
</details>

##### `[1](): any`

<details><summary>Code</summary>

```ts
[1]?();
```
</details>

##### `[2](): void`

<details><summary>Code</summary>

```ts
[2]?() {}
```
</details>

##### `['literal1'](): any`

<details><summary>Code</summary>

```ts
['literal1']?();
```
</details>

##### `['literal2'](): void`

<details><summary>Code</summary>

```ts
['literal2']?() {}
```
</details>

##### `[obj.member](): void`

<details><summary>Code</summary>

```ts
[obj.member]?() {}
```
</details>

##### `[obj.member2](): any`

<details><summary>Code</summary>

```ts
[obj.member2]?();
```
</details>

##### `[f()](): void`

<details><summary>Code</summary>

```ts
[f()]?() {}
```
</details>


---