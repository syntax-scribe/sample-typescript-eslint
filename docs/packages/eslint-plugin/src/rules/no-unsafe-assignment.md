[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-assignment.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-assignment.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getContextualType` | `../util` |
| `getParserServices` | `../util` |
| `getThisExpression` | `../util` |
| `isTypeAnyArrayType` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeUnknownType` | `../util` |
| `isUnsafeAssignment` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `checkArrayDestructureHelper(receiverNode: TSESTree.Node, senderNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function checkArrayDestructureHelper(
      receiverNode: TSESTree.Node,
      senderNode: TSESTree.Node,
    ): boolean {
      if (receiverNode.type !== AST_NODE_TYPES.ArrayPattern) {
        return false;
      }

      const senderTsNode = services.esTreeNodeToTSNodeMap.get(senderNode);
      const senderType = services.getTypeAtLocation(senderNode);

      return checkArrayDestructure(receiverNode, senderType, senderTsNode);
    }
```
</details>

- **Parameters**:
  - `receiverNode: TSESTree.Node`
  - `senderNode: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `services.getTypeAtLocation`
  - `checkArrayDestructure`
### `checkArrayDestructure(receiverNode: TSESTree.ArrayPattern, senderType: ts.Type, senderNode: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function checkArrayDestructure(
      receiverNode: TSESTree.ArrayPattern,
      senderType: ts.Type,
      senderNode: ts.Node,
    ): boolean {
      // any array
      // const [x] = ([] as any[]);
      if (isTypeAnyArrayType(senderType, checker)) {
        context.report({
          node: receiverNode,
          messageId: 'unsafeArrayPattern',
          data: createData(senderType),
        });
        return false;
      }

      if (!checker.isTupleType(senderType)) {
        return true;
      }

      const tupleElements = checker.getTypeArguments(senderType);

      // tuple with any
      // const [x] = [1 as any];
      let didReport = false;
      for (
        let receiverIndex = 0;
        receiverIndex < receiverNode.elements.length;
        receiverIndex += 1
      ) {
        const receiverElement = receiverNode.elements[receiverIndex];
        if (!receiverElement) {
          continue;
        }

        if (receiverElement.type === AST_NODE_TYPES.RestElement) {
          // don't handle rests as they're not a 1:1 assignment
          continue;
        }

        const senderType = tupleElements[receiverIndex] as ts.Type | undefined;
        if (!senderType) {
          continue;
        }

        // check for the any type first so we can handle [[[x]]] = [any]
        if (isTypeAnyType(senderType)) {
          context.report({
            node: receiverElement,
            messageId: 'unsafeArrayPatternFromTuple',
            data: createData(senderType),
          });
          // we want to report on every invalid element in the tuple
          didReport = true;
        } else if (receiverElement.type === AST_NODE_TYPES.ArrayPattern) {
          didReport = checkArrayDestructure(
            receiverElement,
            senderType,
            senderNode,
          );
        } else if (receiverElement.type === AST_NODE_TYPES.ObjectPattern) {
          didReport = checkObjectDestructure(
            receiverElement,
            senderType,
            senderNode,
          );
        }
      }

      return didReport;
    }
```
</details>

- **Parameters**:
  - `receiverNode: TSESTree.ArrayPattern`
  - `senderType: ts.Type`
  - `senderNode: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeAnyArrayType (from ../util)`
  - `context.report`
  - `createData`
  - `checker.isTupleType`
  - `checker.getTypeArguments`
  - `isTypeAnyType (from ../util)`
  - `checkArrayDestructure`
  - `checkObjectDestructure`
- **Internal Comments**:
```
// any array
// const [x] = ([] as any[]);
// tuple with any (x2)
// const [x] = [1 as any]; (x2)
// don't handle rests as they're not a 1:1 assignment
// check for the any type first so we can handle [[[x]]] = [any]
// we want to report on every invalid element in the tuple (x3)
```

### `checkObjectDestructureHelper(receiverNode: TSESTree.Node, senderNode: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function checkObjectDestructureHelper(
      receiverNode: TSESTree.Node,
      senderNode: TSESTree.Node,
    ): boolean {
      if (receiverNode.type !== AST_NODE_TYPES.ObjectPattern) {
        return false;
      }

      const senderTsNode = services.esTreeNodeToTSNodeMap.get(senderNode);
      const senderType = services.getTypeAtLocation(senderNode);

      return checkObjectDestructure(receiverNode, senderType, senderTsNode);
    }
```
</details>

- **Parameters**:
  - `receiverNode: TSESTree.Node`
  - `senderNode: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `services.getTypeAtLocation`
  - `checkObjectDestructure`
### `checkObjectDestructure(receiverNode: TSESTree.ObjectPattern, senderType: ts.Type, senderNode: ts.Node): boolean`

<details><summary>Code</summary>

```ts
function checkObjectDestructure(
      receiverNode: TSESTree.ObjectPattern,
      senderType: ts.Type,
      senderNode: ts.Node,
    ): boolean {
      const properties = new Map(
        senderType
          .getProperties()
          .map(property => [
            property.getName(),
            checker.getTypeOfSymbolAtLocation(property, senderNode),
          ]),
      );

      let didReport = false;
      for (const receiverProperty of receiverNode.properties) {
        if (receiverProperty.type === AST_NODE_TYPES.RestElement) {
          // don't bother checking rest
          continue;
        }

        let key: string;
        if (!receiverProperty.computed) {
          key =
            receiverProperty.key.type === AST_NODE_TYPES.Identifier
              ? receiverProperty.key.name
              : String(receiverProperty.key.value);
        } else if (receiverProperty.key.type === AST_NODE_TYPES.Literal) {
          key = String(receiverProperty.key.value);
        } else if (
          receiverProperty.key.type === AST_NODE_TYPES.TemplateLiteral &&
          receiverProperty.key.quasis.length === 1
        ) {
          key = receiverProperty.key.quasis[0].value.cooked;
        } else {
          // can't figure out the name, so skip it
          continue;
        }

        const senderType = properties.get(key);
        if (!senderType) {
          continue;
        }

        // check for the any type first so we can handle {x: {y: z}} = {x: any}
        if (isTypeAnyType(senderType)) {
          context.report({
            node: receiverProperty.value,
            messageId: 'unsafeArrayPatternFromTuple',
            data: createData(senderType),
          });
          didReport = true;
        } else if (
          receiverProperty.value.type === AST_NODE_TYPES.ArrayPattern
        ) {
          didReport = checkArrayDestructure(
            receiverProperty.value,
            senderType,
            senderNode,
          );
        } else if (
          receiverProperty.value.type === AST_NODE_TYPES.ObjectPattern
        ) {
          didReport = checkObjectDestructure(
            receiverProperty.value,
            senderType,
            senderNode,
          );
        }
      }

      return didReport;
    }
```
</details>

- **Parameters**:
  - `receiverNode: TSESTree.ObjectPattern`
  - `senderType: ts.Type`
  - `senderNode: ts.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `senderType
          .getProperties()
          .map`
  - `property.getName`
  - `checker.getTypeOfSymbolAtLocation`
  - `String`
  - `properties.get`
  - `isTypeAnyType (from ../util)`
  - `context.report`
  - `createData`
  - `checkArrayDestructure`
  - `checkObjectDestructure`
- **Internal Comments**:
```
// don't bother checking rest
// can't figure out the name, so skip it
// check for the any type first so we can handle {x: {y: z}} = {x: any}
```

### `checkAssignment(receiverNode: TSESTree.Node, senderNode: TSESTree.Expression, reportingNode: TSESTree.Node, comparisonType: ComparisonType): boolean`

<details><summary>Code</summary>

```ts
function checkAssignment(
      receiverNode: TSESTree.Node,
      senderNode: TSESTree.Expression,
      reportingNode: TSESTree.Node,
      comparisonType: ComparisonType,
    ): boolean {
      const receiverTsNode = services.esTreeNodeToTSNodeMap.get(receiverNode);
      const receiverType =
        comparisonType === ComparisonType.Contextual
          ? (getContextualType(checker, receiverTsNode as ts.Expression) ??
            services.getTypeAtLocation(receiverNode))
          : services.getTypeAtLocation(receiverNode);
      const senderType = services.getTypeAtLocation(senderNode);

      if (isTypeAnyType(senderType)) {
        // handle cases when we assign any ==> unknown.
        if (isTypeUnknownType(receiverType)) {
          return false;
        }

        let messageId: 'anyAssignment' | 'anyAssignmentThis' = 'anyAssignment';

        if (!isNoImplicitThis) {
          // `var foo = this`
          const thisExpression = getThisExpression(senderNode);
          if (
            thisExpression &&
            isTypeAnyType(
              getConstrainedTypeAtLocation(services, thisExpression),
            )
          ) {
            messageId = 'anyAssignmentThis';
          }
        }

        context.report({
          node: reportingNode,
          messageId,
          data: createData(senderType),
        });

        return true;
      }

      if (comparisonType === ComparisonType.None) {
        return false;
      }

      const result = isUnsafeAssignment(
        senderType,
        receiverType,
        checker,
        senderNode,
      );
      if (!result) {
        return false;
      }

      const { receiver, sender } = result;
      context.report({
        node: reportingNode,
        messageId: 'unsafeAssignment',
        data: createData(sender, receiver),
      });
      return true;
    }
```
</details>

- **Parameters**:
  - `receiverNode: TSESTree.Node`
  - `senderNode: TSESTree.Expression`
  - `reportingNode: TSESTree.Node`
  - `comparisonType: ComparisonType`
- **Return Type**: `boolean`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `getContextualType (from ../util)`
  - `services.getTypeAtLocation`
  - `isTypeAnyType (from ../util)`
  - `isTypeUnknownType (from ../util)`
  - `getThisExpression (from ../util)`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `context.report`
  - `createData`
  - `isUnsafeAssignment (from ../util)`
- **Internal Comments**:
```
// handle cases when we assign any ==> unknown.
// `var foo = this` (x2)
```

### `getComparisonType(typeAnnotation: TSESTree.TSTypeAnnotation | undefined): ComparisonType`

<details><summary>Code</summary>

```ts
function getComparisonType(
      typeAnnotation: TSESTree.TSTypeAnnotation | undefined,
    ): ComparisonType {
      return typeAnnotation
        ? // if there's a type annotation, we can do a comparison
          ComparisonType.Basic
        : // no type annotation means the variable's type will just be inferred, thus equal
          ComparisonType.None;
    }
```
</details>

- **Parameters**:
  - `typeAnnotation: TSESTree.TSTypeAnnotation | undefined`
- **Return Type**: `ComparisonType`
### `createData(senderType: ts.Type, receiverType: ts.Type): Readonly<Record<string, unknown>> | undefined`

<details><summary>Code</summary>

```ts
function createData(
      senderType: ts.Type,
      receiverType?: ts.Type,
    ): Readonly<Record<string, unknown>> | undefined {
      if (receiverType) {
        return {
          receiver: `\`${checker.typeToString(receiverType)}\``,
          sender: `\`${checker.typeToString(senderType)}\``,
        };
      }
      return {
        sender: tsutils.isIntrinsicErrorType(senderType)
          ? 'error typed'
          : '`any`',
      };
    }
```
</details>

- **Parameters**:
  - `senderType: ts.Type`
  - `receiverType: ts.Type`
- **Return Type**: `Readonly<Record<string, unknown>> | undefined`
- **Calls**:
  - `checker.typeToString`
  - `tsutils.isIntrinsicErrorType`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---