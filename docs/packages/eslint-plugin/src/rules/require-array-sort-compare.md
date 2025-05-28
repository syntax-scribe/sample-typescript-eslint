[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `require-array-sort-compare.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
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
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/require-array-sort-compare.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getTypeName` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |
| `isTypeArrayTypeOrUnionOfArrayTypes` | `../util` |


---

## Functions

### `isStringArrayNode(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isStringArrayNode(node: TSESTree.Expression): boolean {
      const type = services.getTypeAtLocation(node);

      if (checker.isArrayType(type) || checker.isTupleType(type)) {
        const typeArgs = checker.getTypeArguments(type);
        return typeArgs.every(arg => getTypeName(checker, arg) === 'string');
      }
      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a given node is an array which all elements are string.
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `checker.isArrayType`
  - `checker.isTupleType`
  - `checker.getTypeArguments`
  - `typeArgs.every`
  - `getTypeName (from ../util)`
### `checkSortArgument(callee: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
function checkSortArgument(callee: TSESTree.MemberExpression): void {
      if (!isStaticMemberAccessOfValue(callee, context, 'sort', 'toSorted')) {
        return;
      }
      const calleeObjType = getConstrainedTypeAtLocation(
        services,
        callee.object,
      );

      if (options.ignoreStringArrays && isStringArrayNode(callee.object)) {
        return;
      }

      if (isTypeArrayTypeOrUnionOfArrayTypes(calleeObjType, checker)) {
        context.report({ node: callee.parent, messageId: 'requireCompare' });
      }
    }
```
</details>

- **Parameters**:
  - `callee: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `isStaticMemberAccessOfValue (from ../util)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `isStringArrayNode`
  - `isTypeArrayTypeOrUnionOfArrayTypes (from ../util)`
  - `context.report`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    ignoreStringArrays?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'requireCompare';
```


---