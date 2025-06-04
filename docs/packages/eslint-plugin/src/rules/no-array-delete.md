[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-array-delete.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 5 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-array-delete.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `shouldHaveParentheses` | `boolean` | const | `property.type === AST_NODE_TYPES.SequenceExpression` | ✗ |
| `nodeMap` | `any` | const | `services.esTreeNodeToTSNodeMap` | ✗ |
| `key` | `any` | const | `shouldHaveParentheses ? `(${rawKey})` : rawKey` | ✗ |
| `suggestion` | `string` | let/var | ``${target}.splice(${key}, 1)`` | ✗ |
| `indentationCount` | `any` | const | `node.loc.start.column` | ✗ |


---

## Functions

### `isUnderlyingTypeArray(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isUnderlyingTypeArray(type: ts.Type): boolean {
      const predicate = (t: ts.Type): boolean =>
        checker.isArrayType(t) || checker.isTupleType(t);

      if (type.isUnion()) {
        return type.types.every(predicate);
      }

      if (type.isIntersection()) {
        return type.types.some(predicate);
      }

      return predicate(type);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.isArrayType`
  - `checker.isTupleType`
  - `type.isUnion`
  - `type.types.every`
  - `type.isIntersection`
  - `type.types.some`
  - `predicate`
### `predicate(t: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(t: ts.Type): boolean =>
        checker.isArrayType(t) || checker.isTupleType(t)
```
</details>

- **Parameters**:
  - `t: ts.Type`
- **Return Type**: `boolean`

---

## Type Aliases

### `MessageId`

```ts
type MessageId = 'noArrayDelete' | 'useSplice';
```


---