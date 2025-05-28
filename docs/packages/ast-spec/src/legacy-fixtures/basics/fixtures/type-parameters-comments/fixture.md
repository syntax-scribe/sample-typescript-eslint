[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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