[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `restrict-plus-operands.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 2 |
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
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/restrict-plus-operands.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getTypeName` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeFlagSet` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `stringLike` | `string` | const | `stringLikes.length
      ? stringLikes.length === 1
        ? `string, allowing a string + ${stringLikes[0]}`
        : `string, allowing a string + any of: ${stringLikes.join(', ')}`
      : 'string'` | ✗ |
| `hadIndividualComplaint` | `boolean` | let/var | `false` | ✗ |


---

## Functions

### `getTypeConstrained(node: TSESTree.Node): ts.Type`

<details><summary>Code</summary>

```ts
function getTypeConstrained(node: TSESTree.Node): ts.Type {
      return typeChecker.getBaseTypeOfLiteralType(
        getConstrainedTypeAtLocation(services, node),
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `ts.Type`
- **Calls**:
  - `typeChecker.getBaseTypeOfLiteralType`
  - `getConstrainedTypeAtLocation (from ../util)`
### `checkPlusOperands(node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression): void`

<details><summary>Code</summary>

```ts
function checkPlusOperands(
      node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression,
    ): void {
      const leftType = getTypeConstrained(node.left);
      const rightType = getTypeConstrained(node.right);

      if (
        leftType === rightType &&
        tsutils.isTypeFlagSet(
          leftType,
          ts.TypeFlags.BigIntLike |
            ts.TypeFlags.NumberLike |
            ts.TypeFlags.StringLike,
        )
      ) {
        return;
      }

      let hadIndividualComplaint = false;

      for (const [baseNode, baseType, otherType] of [
        [node.left, leftType, rightType],
        [node.right, rightType, leftType],
      ] as const) {
        if (
          isTypeFlagSetInUnion(
            baseType,
            ts.TypeFlags.ESSymbolLike |
              ts.TypeFlags.Never |
              ts.TypeFlags.Unknown,
          ) ||
          (!allowAny && isTypeFlagSetInUnion(baseType, ts.TypeFlags.Any)) ||
          (!allowBoolean &&
            isTypeFlagSetInUnion(baseType, ts.TypeFlags.BooleanLike)) ||
          (!allowNullish &&
            isTypeFlagSet(baseType, ts.TypeFlags.Null | ts.TypeFlags.Undefined))
        ) {
          context.report({
            node: baseNode,
            messageId: 'invalid',
            data: {
              type: typeChecker.typeToString(baseType),
              stringLike,
            },
          });
          hadIndividualComplaint = true;
          continue;
        }

        // RegExps also contain ts.TypeFlags.Any & ts.TypeFlags.Object
        for (const subBaseType of tsutils.unionConstituents(baseType)) {
          const typeName = getTypeName(typeChecker, subBaseType);
          if (
            typeName === 'RegExp'
              ? !allowRegExp ||
                tsutils.isTypeFlagSet(otherType, ts.TypeFlags.NumberLike)
              : (!allowAny && isTypeAnyType(subBaseType)) ||
                isDeeplyObjectType(subBaseType)
          ) {
            context.report({
              node: baseNode,
              messageId: 'invalid',
              data: {
                type: typeChecker.typeToString(subBaseType),
                stringLike,
              },
            });
            hadIndividualComplaint = true;
            continue;
          }
        }
      }

      if (hadIndividualComplaint) {
        return;
      }

      for (const [baseType, otherType] of [
        [leftType, rightType],
        [rightType, leftType],
      ] as const) {
        if (
          !allowNumberAndString &&
          isTypeFlagSetInUnion(baseType, ts.TypeFlags.StringLike) &&
          isTypeFlagSetInUnion(
            otherType,
            ts.TypeFlags.NumberLike | ts.TypeFlags.BigIntLike,
          )
        ) {
          return context.report({
            node,
            messageId: 'mismatched',
            data: {
              left: typeChecker.typeToString(leftType),
              right: typeChecker.typeToString(rightType),
              stringLike,
            },
          });
        }

        if (
          isTypeFlagSetInUnion(baseType, ts.TypeFlags.NumberLike) &&
          isTypeFlagSetInUnion(otherType, ts.TypeFlags.BigIntLike)
        ) {
          return context.report({
            node,
            messageId: 'bigintAndNumber',
            data: {
              left: typeChecker.typeToString(leftType),
              right: typeChecker.typeToString(rightType),
            },
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression | TSESTree.BinaryExpression`
- **Return Type**: `void`
- **Calls**:
  - `getTypeConstrained`
  - `tsutils.isTypeFlagSet`
  - `isTypeFlagSetInUnion`
  - `isTypeFlagSet (from ../util)`
  - `context.report`
  - `typeChecker.typeToString`
  - `tsutils.unionConstituents`
  - `getTypeName (from ../util)`
  - `isTypeAnyType (from ../util)`
  - `isDeeplyObjectType`
- **Internal Comments**:
```
// RegExps also contain ts.TypeFlags.Any & ts.TypeFlags.Object
```

### `isDeeplyObjectType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isDeeplyObjectType(type: ts.Type): boolean {
  return type.isIntersection()
    ? tsutils.intersectionConstituents(type).every(tsutils.isObjectType)
    : tsutils.unionConstituents(type).every(tsutils.isObjectType);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isIntersection`
  - `tsutils.intersectionConstituents(type).every`
  - `tsutils.unionConstituents(type).every`
### `isTypeFlagSetInUnion(type: ts.Type, flag: ts.TypeFlags): boolean`

<details><summary>Code</summary>

```ts
function isTypeFlagSetInUnion(type: ts.Type, flag: ts.TypeFlags): boolean {
  return tsutils
    .unionConstituents(type)
    .some(subType => tsutils.isTypeFlagSet(subType, flag));
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `flag: ts.TypeFlags`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
    .unionConstituents(type)
    .some`
  - `tsutils.isTypeFlagSet`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowAny?: boolean;
    allowBoolean?: boolean;
    allowNullish?: boolean;
    allowNumberAndString?: boolean;
    allowRegExp?: boolean;
    skipCompoundAssignments?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'bigintAndNumber' | 'invalid' | 'mismatched';
```


---