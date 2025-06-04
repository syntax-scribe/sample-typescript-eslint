[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 2 |
| 📐 Interfaces | 2 |

## 📚 Table of Contents

- [Classes](#classes)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-parameters-comments-heritage/fixture.ts`**

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