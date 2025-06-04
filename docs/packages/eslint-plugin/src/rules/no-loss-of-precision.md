[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-loss-of-precision.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📑 Type Aliases | 2 |

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