[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Classes](#classes)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 2
- **Imports**: 0
- **Interfaces**: 2
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-parameters-comments-heritage/fixture.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `foo`

<details><summary>Class Code</summary>

```ts
class foo</* aaa */ A /* bbb */> extends bar</* aaa */ A /* bbb */> {}
```
</details>

### `foo2`

<details><summary>Class Code</summary>

```ts
class foo2<
  /* aaa */ A /* bbb */ = 2 /* bbb */,
> extends bar</* aaa */ A /* bbb */> {}
```
</details>


---

## Interfaces

### `bar<A>`

<details><summary>Interface Code</summary>

```ts
interface bar</* aaa */ A /* bbb */> extends bar2</* aaa */ A /* bbb */> {}
```
</details>

### `bar2<A /* bbb */ = 2>`

<details><summary>Interface Code</summary>

```ts
interface bar2</* aaa */ A /* bbb */ = 2 /* bbb */>
  extends bar</* aaa */ A /* bbb */> {}
```
</details>


---

## Type Aliases

> No type aliases found in this file.


---