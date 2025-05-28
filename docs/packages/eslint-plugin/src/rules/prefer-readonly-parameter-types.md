[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-readonly-parameter-types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 1 |
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

## 🔧 Functions

> No functions found in this file.


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