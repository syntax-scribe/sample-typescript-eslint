[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-destructuring.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 10
- **Interfaces**: 0
- **Type Aliases**: 5

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-destructuring.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isTypeAnyType` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `performCheck(leftNode: TSESTree.BindingName | TSESTree.Expression, rightNode: TSESTree.Expression | null, reportNode: TSESTree.AssignmentExpression | TSESTree.VariableDeclarator): void`

<details><summary>Code</summary>

```ts
function performCheck(
      leftNode: TSESTree.BindingName | TSESTree.Expression,
      rightNode: TSESTree.Expression | null,
      reportNode: TSESTree.AssignmentExpression | TSESTree.VariableDeclarator,
    ): void {
      const rules =
        leftNode.type === AST_NODE_TYPES.Identifier &&
        leftNode.typeAnnotation == null
          ? baseRules
          : baseRulesWithoutFix();
      if (
        (leftNode.type === AST_NODE_TYPES.ArrayPattern ||
          leftNode.type === AST_NODE_TYPES.Identifier ||
          leftNode.type === AST_NODE_TYPES.ObjectPattern) &&
        leftNode.typeAnnotation != null &&
        !enforceForDeclarationWithTypeAnnotation
      ) {
        return;
      }

      if (
        rightNode != null &&
        isArrayLiteralIntegerIndexAccess(rightNode) &&
        rightNode.object.type !== AST_NODE_TYPES.Super
      ) {
        const tsObj = esTreeNodeToTSNodeMap.get(rightNode.object);
        const objType = typeChecker.getTypeAtLocation(tsObj);
        if (!isTypeAnyOrIterableType(objType, typeChecker)) {
          if (
            !enforceForRenamedProperties ||
            !getNormalizedEnabledType(reportNode.type, 'object')
          ) {
            return;
          }
          context.report({
            node: reportNode,
            messageId: 'preferDestructuring',
            data: { type: 'object' },
          });
          return;
        }
      }

      if (reportNode.type === AST_NODE_TYPES.AssignmentExpression) {
        rules.AssignmentExpression(reportNode);
      } else {
        rules.VariableDeclarator(reportNode);
      }
    }
```
</details>

- **Parameters**:
  - `leftNode: TSESTree.BindingName | TSESTree.Expression`
  - `rightNode: TSESTree.Expression | null`
  - `reportNode: TSESTree.AssignmentExpression | TSESTree.VariableDeclarator`
- **Return Type**: `void`
- **Calls**:
  - `baseRulesWithoutFix`
  - `isArrayLiteralIntegerIndexAccess`
  - `esTreeNodeToTSNodeMap.get`
  - `typeChecker.getTypeAtLocation`
  - `isTypeAnyOrIterableType`
  - `getNormalizedEnabledType`
  - `context.report`
  - `rules.AssignmentExpression`
  - `rules.VariableDeclarator`
### `getNormalizedEnabledType(nodeType: | AST_NODE_TYPES.AssignmentExpression
        | AST_NODE_TYPES.VariableDeclarator, destructuringType: 'array' | 'object'): boolean | undefined`

<details><summary>Code</summary>

```ts
function getNormalizedEnabledType(
      nodeType:
        | AST_NODE_TYPES.AssignmentExpression
        | AST_NODE_TYPES.VariableDeclarator,
      destructuringType: 'array' | 'object',
    ): boolean | undefined {
      if ('object' in enabledTypes || 'array' in enabledTypes) {
        return enabledTypes[destructuringType];
      }
      return enabledTypes[nodeType as keyof typeof enabledTypes][
        destructuringType as keyof (typeof enabledTypes)[keyof typeof enabledTypes]
      ];
    }
```
</details>

- **Parameters**:
  - `nodeType: | AST_NODE_TYPES.AssignmentExpression
        | AST_NODE_TYPES.VariableDeclarator`
  - `destructuringType: 'array' | 'object'`
- **Return Type**: `boolean | undefined`
### `baseRulesWithoutFix(): ReturnType<typeof baseRule.create>`

<details><summary>Code</summary>

```ts
function baseRulesWithoutFix(): ReturnType<typeof baseRule.create> {
      baseRulesWithoutFixCache ??= baseRule.create(noFixContext(context));
      return baseRulesWithoutFixCache;
    }
```
</details>

- **Return Type**: `ReturnType<typeof baseRule.create>`
- **Calls**:
  - `baseRule.create`
  - `noFixContext`
### `noFixContext(context: Context): Context`

<details><summary>Code</summary>

```ts
function noFixContext(context: Context): Context {
  const customContext: {
    report: Context['report'];
  } = {
    report: (descriptor): void => {
      context.report({
        ...descriptor,
        fix: undefined,
      });
    },
  };

  // we can't directly proxy `context` because its `report` property is non-configurable
  // and non-writable. So we proxy `customContext` and redirect all
  // property access to the original context except for `report`
  return new Proxy<Context>(customContext as typeof context, {
    get(target, path, receiver): unknown {
      if (path !== 'report') {
        return Reflect.get(context, path, receiver);
      }
      return Reflect.get(target, path, receiver);
    },
  });
}
```
</details>

- **Parameters**:
  - `context: Context`
- **Return Type**: `Context`
- **Calls**:
  - `context.report`
  - `Reflect.get`
- **Internal Comments**:
```
// we can't directly proxy `context` because its `report` property is non-configurable
// and non-writable. So we proxy `customContext` and redirect all
// property access to the original context except for `report`
```

### `report(descriptor: any): void`

<details><summary>Code</summary>

```ts
(descriptor): void => {
      context.report({
        ...descriptor,
        fix: undefined,
      });
    }
```
</details>

- **Parameters**:
  - `descriptor: any`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `report(descriptor: any): void`

<details><summary>Code</summary>

```ts
(descriptor): void => {
      context.report({
        ...descriptor,
        fix: undefined,
      });
    }
```
</details>

- **Parameters**:
  - `descriptor: any`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `report(descriptor: any): void`

<details><summary>Code</summary>

```ts
(descriptor): void => {
      context.report({
        ...descriptor,
        fix: undefined,
      });
    }
```
</details>

- **Parameters**:
  - `descriptor: any`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `isTypeAnyOrIterableType(type: ts.Type, typeChecker: ts.TypeChecker): boolean`

<details><summary>Code</summary>

```ts
function isTypeAnyOrIterableType(
  type: ts.Type,
  typeChecker: ts.TypeChecker,
): boolean {
  if (isTypeAnyType(type)) {
    return true;
  }
  if (!type.isUnion()) {
    const iterator = tsutils.getWellKnownSymbolPropertyOfType(
      type,
      'iterator',
      typeChecker,
    );
    return iterator != null;
  }
  return type.types.every(t => isTypeAnyOrIterableType(t, typeChecker));
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `typeChecker: ts.TypeChecker`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeAnyType (from ../util)`
  - `type.isUnion`
  - `tsutils.getWellKnownSymbolPropertyOfType`
  - `type.types.every`
  - `isTypeAnyOrIterableType`
### `isArrayLiteralIntegerIndexAccess(node: TSESTree.Expression): node is TSESTree.MemberExpression`

<details><summary>Code</summary>

```ts
function isArrayLiteralIntegerIndexAccess(
  node: TSESTree.Expression,
): node is TSESTree.MemberExpression {
  if (node.type !== AST_NODE_TYPES.MemberExpression) {
    return false;
  }
  if (node.property.type !== AST_NODE_TYPES.Literal) {
    return false;
  }
  return Number.isInteger(node.property.value);
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `node is TSESTree.MemberExpression`
- **Calls**:
  - `Number.isInteger`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `BaseOptions`

```ts
type BaseOptions = InferOptionsTypeFromRule<typeof baseRule>;
```

### `EnforcementOptions`

```ts
type EnforcementOptions = {
  enforceForDeclarationWithTypeAnnotation?: boolean;
} & BaseOptions[1];
```

### `Options`

```ts
type Options = [BaseOptions[0], EnforcementOptions];
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```

### `Context`

```ts
type Context = TSESLint.RuleContext<MessageIds, Options>;
```


---