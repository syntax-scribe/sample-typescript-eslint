[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-loss-of-precision.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-loss-of-precision.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---


---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<NonNullable<typeof baseRule>>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<
  NonNullable<typeof baseRule>
>;
```


---