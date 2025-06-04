[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/type-parameters-comments/fixture.ts`**

## Functions

### `bar(): void`

<details><summary>Code</summary>

```ts
function bar</* aaa */ A /* bbb */>() {}
```
</details>

- **Return Type**: `void`
### `baz(): void`

<details><summary>Code</summary>

```ts
function baz</* aaa */ A /* bbb */ = Foo>() {}
```
</details>

- **Return Type**: `void`

---