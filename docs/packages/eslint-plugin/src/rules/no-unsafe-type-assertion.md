[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-type-assertion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-type-assertion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeUnknownType` | `../util` |
| `isUnsafeAssignment` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `expressionWidenedType` | `any` | const | `isObjectLiteralType(expressionType)
        ? checker.getWidenedType(expressionType)
        : expressionType` | ✗ |


---

## Functions

### `getAnyTypeName(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function getAnyTypeName(type: ts.Type): string {
      return tsutils.isIntrinsicErrorType(type) ? 'error typed' : '`any`';
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `tsutils.isIntrinsicErrorType`
### `isObjectLiteralType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isObjectLiteralType(type: ts.Type): boolean {
      return (
        tsutils.isObjectType(type) &&
        tsutils.isObjectFlagSet(type, ts.ObjectFlags.ObjectLiteral)
      );
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.isObjectType`
  - `tsutils.isObjectFlagSet`
### `checkExpression(node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion): void`

<details><summary>Code</summary>

```ts
function checkExpression(
      node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion,
    ): void {
      const expressionType = services.getTypeAtLocation(node.expression);
      const assertedType = services.getTypeAtLocation(node.typeAnnotation);

      if (expressionType === assertedType) {
        return;
      }

      // handle cases when asserting unknown ==> any.
      if (isTypeAnyType(assertedType) && isTypeUnknownType(expressionType)) {
        context.report({
          node,
          messageId: 'unsafeToAnyTypeAssertion',
          data: {
            type: '`any`',
          },
        });

        return;
      }

      const unsafeExpressionAny = isUnsafeAssignment(
        expressionType,
        assertedType,
        checker,
        node.expression,
      );

      if (unsafeExpressionAny) {
        context.report({
          node,
          messageId: 'unsafeOfAnyTypeAssertion',
          data: {
            type: getAnyTypeName(unsafeExpressionAny.sender),
          },
        });

        return;
      }

      const unsafeAssertedAny = isUnsafeAssignment(
        assertedType,
        expressionType,
        checker,
        node.typeAnnotation,
      );

      if (unsafeAssertedAny) {
        context.report({
          node,
          messageId: 'unsafeToAnyTypeAssertion',
          data: {
            type: getAnyTypeName(unsafeAssertedAny.sender),
          },
        });

        return;
      }

      // Use the widened type in case of an object literal so `isTypeAssignableTo()`
      // won't fail on excess property check.
      const expressionWidenedType = isObjectLiteralType(expressionType)
        ? checker.getWidenedType(expressionType)
        : expressionType;

      const isAssertionSafe = checker.isTypeAssignableTo(
        expressionWidenedType,
        assertedType,
      );
      if (isAssertionSafe) {
        return;
      }

      // Produce a more specific error message when targeting a type parameter
      if (tsutils.isTypeParameter(assertedType)) {
        const assertedTypeConstraint =
          checker.getBaseConstraintOfType(assertedType);
        if (!assertedTypeConstraint) {
          // asserting to an unconstrained type parameter is unsafe
          context.report({
            node,
            messageId: 'unsafeToUnconstrainedTypeAssertion',
            data: {
              type: checker.typeToString(assertedType),
            },
          });
          return;
        }

        // special case message if the original type is assignable to the
        // constraint of the target type parameter
        const isAssignableToConstraint = checker.isTypeAssignableTo(
          expressionWidenedType,
          assertedTypeConstraint,
        );
        if (isAssignableToConstraint) {
          context.report({
            node,
            messageId: 'unsafeTypeAssertionAssignableToConstraint',
            data: {
              type: checker.typeToString(assertedType),
            },
          });
          return;
        }
      }

      // General error message
      context.report({
        node,
        messageId: 'unsafeTypeAssertion',
        data: {
          type: checker.typeToString(assertedType),
        },
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `services.getTypeAtLocation`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `context.report`
  - `isUnsafeAssignment (from ../util)`
  - `getAnyTypeName`
  - `isObjectLiteralType`
  - `checker.getWidenedType`
  - `checker.isTypeAssignableTo`
  - `tsutils.isTypeParameter`
  - `checker.getBaseConstraintOfType`
  - `checker.typeToString`
- **Internal Comments**:
```
// handle cases when asserting unknown ==> any.
// Use the widened type in case of an object literal so `isTypeAssignableTo()` (x2)
// won't fail on excess property check. (x2)
// Produce a more specific error message when targeting a type parameter
// asserting to an unconstrained type parameter is unsafe (x4)
// special case message if the original type is assignable to the (x2)
// constraint of the target type parameter (x2)
// General error message (x4)
```


---