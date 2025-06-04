[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-invalid-this.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 6 |
| 📊 Variables & Constants | 3 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-invalid-this.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultOptions` | `Options` | const | `[{ capIsConstructor: true }]` | ✗ |
| `thisIsValidStack` | `boolean[]` | const | `[]` | ✗ |
| `thisIsValidHere` | `boolean` | const | `thisIsValidStack[thisIsValidStack.length - 1]` | ✗ |


---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---