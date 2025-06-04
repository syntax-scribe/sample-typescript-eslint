[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-readonly-parameter-types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 8 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-readonly-parameter-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isTypeReadonly` | `../util` |
| `readonlynessOptionsDefaults` | `../util` |
| `readonlynessOptionsSchema` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `actualParam` | `any` | const | `param.type === AST_NODE_TYPES.TSParameterProperty
              ? param.parameter
              : param` | ✗ |


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allow?: TypeOrValueSpecifier[];
    checkParameterProperties?: boolean;
    ignoreInferredTypes?: boolean;
    treatMethodsAsReadonly?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'shouldBeReadonly';
```


---