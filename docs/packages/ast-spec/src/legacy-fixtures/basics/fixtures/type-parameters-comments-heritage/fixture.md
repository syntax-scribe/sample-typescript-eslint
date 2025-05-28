[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 2 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Classes](#classes)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-parameters-comments-heritage/fixture.ts`**

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