[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `InferTypesFromRule.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/InferTypesFromRule.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleCreateFunction` | `../ts-eslint` |
| `RuleModule` | `../ts-eslint` |


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

### `InferOptionsTypeFromRule<T>`

/**
 * Uses type inference to fetch the Options type from the given RuleModule
 */

```ts
type InferOptionsTypeFromRule<T> = T extends RuleModule<infer _MessageIds, infer Options>
    ? Options
    : T extends RuleCreateFunction<infer _MessageIds, infer Options>
      ? Options
      : unknown;
```

### `InferMessageIdsTypeFromRule<T>`

/**
 * Uses type inference to fetch the MessageIds type from the given RuleModule
 */

```ts
type InferMessageIdsTypeFromRule<T> = T extends RuleModule<infer MessageIds, infer _TOptions>
    ? MessageIds
    : T extends RuleCreateFunction<infer MessageIds, infer _TOptions>
      ? MessageIds
      : unknown;
```


---