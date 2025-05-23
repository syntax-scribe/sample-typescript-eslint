[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-readonly-parameter-types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 2

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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