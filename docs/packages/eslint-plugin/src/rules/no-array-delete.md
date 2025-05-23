[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-array-delete.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageId`

```ts
type MessageId = 'noArrayDelete' | 'useSplice';
```


---