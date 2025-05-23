[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-duplicate-type-constituents.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 21
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-duplicate-type-constituents.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `Type` | `typescript` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isFunctionOrFunctionType` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `isSameAstNode(actualNode: unknown, expectedNode: unknown): boolean`

<details><summary>Code</summary>

```ts
(actualNode: unknown, expectedNode: unknown): boolean => {
  if (actualNode === expectedNode) {
    return true;
  }
  if (
    actualNode &&
    expectedNode &&
    typeof actualNode === 'object' &&
    typeof expectedNode === 'object'
  ) {
    if (Array.isArray(actualNode) && Array.isArray(expectedNode)) {
      if (actualNode.length !== expectedNode.length) {
        return false;
      }
      return !actualNode.some(
        (nodeEle, index) => !isSameAstNode(nodeEle, expectedNode[index]),
      );
    }
    const actualNodeKeys = Object.keys(actualNode).filter(
      key => !astIgnoreKeys.has(key),
    );
    const expectedNodeKeys = Object.keys(expectedNode).filter(
      key => !astIgnoreKeys.has(key),
    );
    if (actualNodeKeys.length !== expectedNodeKeys.length) {
      return false;
    }
    if (
      actualNodeKeys.some(
        actualNodeKey => !Object.hasOwn(expectedNode, actualNodeKey),
      )
    ) {
      return false;
    }
    if (
      actualNodeKeys.some(
        actualNodeKey =>
          !isSameAstNode(
            actualNode[actualNodeKey as keyof typeof actualNode],
            expectedNode[actualNodeKey as keyof typeof expectedNode],
          ),
      )
    ) {
      return false;
    }
    return true;
  }
  return false;
}
```
</details>

- **Parameters**:
  - `actualNode: unknown`
  - `expectedNode: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `Array.isArray`
  - `actualNode.some`
  - `isSameAstNode`
  - `Object.keys(actualNode).filter`
  - `astIgnoreKeys.has`
  - `Object.keys(expectedNode).filter`
  - `actualNodeKeys.some`
  - `Object.hasOwn`
### `report(messageId: MessageIds, constituentNode: TSESTree.TypeNode, data: Record<string, unknown>): void`

<details><summary>Code</summary>

```ts
function report(
      messageId: MessageIds,
      constituentNode: TSESTree.TypeNode,
      data?: Record<string, unknown>,
    ): void {
      const getUnionOrIntersectionToken = (
        where: 'After' | 'Before',
        at: number,
      ): TSESTree.Token | undefined =>
        sourceCode[`getTokens${where}`](constituentNode, {
          filter: token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1],
        }).at(at);

      const beforeUnionOrIntersectionToken = getUnionOrIntersectionToken(
        'Before',
        -1,
      );
      let afterUnionOrIntersectionToken: TSESTree.Token | undefined;
      let bracketBeforeTokens;
      let bracketAfterTokens;
      if (beforeUnionOrIntersectionToken) {
        bracketBeforeTokens = sourceCode.getTokensBetween(
          beforeUnionOrIntersectionToken,
          constituentNode,
        );
        bracketAfterTokens = sourceCode.getTokensAfter(constituentNode, {
          count: bracketBeforeTokens.length,
        });
      } else {
        afterUnionOrIntersectionToken = nullThrows(
          getUnionOrIntersectionToken('After', 0),
          NullThrowsReasons.MissingToken(
            'union or intersection token',
            'duplicate type constituent',
          ),
        );
        bracketAfterTokens = sourceCode.getTokensBetween(
          constituentNode,
          afterUnionOrIntersectionToken,
        );
        bracketBeforeTokens = sourceCode.getTokensBefore(constituentNode, {
          count: bracketAfterTokens.length,
        });
      }
      context.report({
        loc: {
          start: constituentNode.loc.start,
          end: (bracketAfterTokens.at(-1) ?? constituentNode).loc.end,
        },
        node: constituentNode,
        messageId,
        data,
        fix: fixer =>
          [
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap(token => (token ? fixer.remove(token) : [])),
      });
    }
```
</details>

- **Parameters**:
  - `messageId: MessageIds`
  - `constituentNode: TSESTree.TypeNode`
  - `data: Record<string, unknown>`
- **Return Type**: `void`
- **Calls**:
  - `sourceCode[`getTokens${where}`](constituentNode, {
          filter: token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1],
        }).at`
  - `getUnionOrIntersectionToken`
  - `sourceCode.getTokensBetween`
  - `sourceCode.getTokensAfter`
  - `nullThrows (from ../util)`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getTokensBefore`
  - `context.report`
  - `bracketAfterTokens.at`
  - `[
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap`
  - `fixer.remove`
### `getUnionOrIntersectionToken(where: 'After' | 'Before', at: number): TSESTree.Token | undefined`

<details><summary>Code</summary>

```ts
(
        where: 'After' | 'Before',
        at: number,
      ): TSESTree.Token | undefined =>
        sourceCode[`getTokens${where}`](constituentNode, {
          filter: token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1],
        }).at(at)
```
</details>

- **Parameters**:
  - `where: 'After' | 'Before'`
  - `at: number`
- **Return Type**: `TSESTree.Token | undefined`
- **Calls**:
  - `sourceCode[`getTokens${where}`](constituentNode, {
          filter: token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1],
        }).at`
### `filter(token: any): boolean`

<details><summary>Code</summary>

```ts
token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1]
```
</details>

- **Parameters**:
  - `token: any`
- **Return Type**: `boolean`
### `filter(token: any): boolean`

<details><summary>Code</summary>

```ts
token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1]
```
</details>

- **Parameters**:
  - `token: any`
- **Return Type**: `boolean`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer =>
          [
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap(token => (token ? fixer.remove(token) : []))
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `[
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer =>
          [
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap(token => (token ? fixer.remove(token) : []))
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `[
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap`
### `checkDuplicateRecursively(unionOrIntersection: UnionOrIntersection, constituentNode: TSESTree.TypeNode, uniqueConstituents: TSESTree.TypeNode[], cachedTypeMap: Map<Type, TSESTree.TypeNode>, forEachNodeType: (type: Type, node: TSESTree.TypeNode) => void): void`

<details><summary>Code</summary>

```ts
function checkDuplicateRecursively(
      unionOrIntersection: UnionOrIntersection,
      constituentNode: TSESTree.TypeNode,
      uniqueConstituents: TSESTree.TypeNode[],
      cachedTypeMap: Map<Type, TSESTree.TypeNode>,
      forEachNodeType?: (type: Type, node: TSESTree.TypeNode) => void,
    ): void {
      const type = parserServices.getTypeAtLocation(constituentNode);
      if (tsutils.isIntrinsicErrorType(type)) {
        return;
      }
      const duplicatedPrevious =
        uniqueConstituents.find(ele => isSameAstNode(ele, constituentNode)) ??
        cachedTypeMap.get(type);

      if (duplicatedPrevious) {
        report('duplicate', constituentNode, {
          type: unionOrIntersection,
          previous: sourceCode.getText(duplicatedPrevious),
        });
        return;
      }

      forEachNodeType?.(type, constituentNode);
      cachedTypeMap.set(type, constituentNode);
      uniqueConstituents.push(constituentNode);

      if (
        (unionOrIntersection === 'Union' &&
          constituentNode.type === AST_NODE_TYPES.TSUnionType) ||
        (unionOrIntersection === 'Intersection' &&
          constituentNode.type === AST_NODE_TYPES.TSIntersectionType)
      ) {
        for (const constituent of constituentNode.types) {
          checkDuplicateRecursively(
            unionOrIntersection,
            constituent,
            uniqueConstituents,
            cachedTypeMap,
            forEachNodeType,
          );
        }
      }
    }
```
</details>

- **Parameters**:
  - `unionOrIntersection: UnionOrIntersection`
  - `constituentNode: TSESTree.TypeNode`
  - `uniqueConstituents: TSESTree.TypeNode[]`
  - `cachedTypeMap: Map<Type, TSESTree.TypeNode>`
  - `forEachNodeType: (type: Type, node: TSESTree.TypeNode) => void`
- **Return Type**: `void`
- **Calls**:
  - `parserServices.getTypeAtLocation`
  - `tsutils.isIntrinsicErrorType`
  - `uniqueConstituents.find`
  - `isSameAstNode`
  - `cachedTypeMap.get`
  - `report`
  - `sourceCode.getText`
  - `forEachNodeType`
  - `cachedTypeMap.set`
  - `uniqueConstituents.push`
  - `checkDuplicateRecursively`
### `checkDuplicate(node: TSESTree.TSIntersectionType | TSESTree.TSUnionType, forEachNodeType: (
        constituentNodeType: Type,
        constituentNode: TSESTree.TypeNode,
      ) => void): void`

<details><summary>Code</summary>

```ts
function checkDuplicate(
      node: TSESTree.TSIntersectionType | TSESTree.TSUnionType,
      forEachNodeType?: (
        constituentNodeType: Type,
        constituentNode: TSESTree.TypeNode,
      ) => void,
    ): void {
      const cachedTypeMap = new Map<Type, TSESTree.TypeNode>();
      const uniqueConstituents: TSESTree.TypeNode[] = [];

      const unionOrIntersection =
        node.type === AST_NODE_TYPES.TSIntersectionType
          ? 'Intersection'
          : 'Union';

      for (const type of node.types) {
        checkDuplicateRecursively(
          unionOrIntersection,
          type,
          uniqueConstituents,
          cachedTypeMap,
          forEachNodeType,
        );
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSIntersectionType | TSESTree.TSUnionType`
  - `forEachNodeType: (
        constituentNodeType: Type,
        constituentNode: TSESTree.TypeNode,
      ) => void`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicateRecursively`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `filter(token: any): boolean`

<details><summary>Code</summary>

```ts
token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1]
```
</details>

- **Parameters**:
  - `token: any`
- **Return Type**: `boolean`
### `filter(token: any): boolean`

<details><summary>Code</summary>

```ts
token =>
            ['&', '|'].includes(token.value) &&
            constituentNode.parent.range[0] <= token.range[0] &&
            token.range[1] <= constituentNode.parent.range[1]
```
</details>

- **Parameters**:
  - `token: any`
- **Return Type**: `boolean`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer =>
          [
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap(token => (token ? fixer.remove(token) : []))
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `[
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer =>
          [
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap(token => (token ? fixer.remove(token) : []))
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
- **Calls**:
  - `[
            beforeUnionOrIntersectionToken,
            ...bracketBeforeTokens,
            constituentNode,
            ...bracketAfterTokens,
            afterUnionOrIntersectionToken,
          ].flatMap`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`
### `TSUnionType(node: any): void`

<details><summary>Code</summary>

```ts
(node): void => {
          if (node.parent.type === AST_NODE_TYPES.TSUnionType) {
            return;
          }
          checkDuplicate(node, (constituentNodeType, constituentNode) => {
            const maybeTypeAnnotation = node.parent;
            if (maybeTypeAnnotation.type === AST_NODE_TYPES.TSTypeAnnotation) {
              const maybeIdentifier = maybeTypeAnnotation.parent;
              if (
                maybeIdentifier.type === AST_NODE_TYPES.Identifier &&
                maybeIdentifier.optional
              ) {
                const maybeFunction = maybeIdentifier.parent;
                if (
                  isFunctionOrFunctionType(maybeFunction) &&
                  maybeFunction.params.includes(maybeIdentifier) &&
                  tsutils.isTypeFlagSet(
                    constituentNodeType,
                    ts.TypeFlags.Undefined,
                  )
                ) {
                  report('unnecessary', constituentNode);
                }
              }
            }
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
- **Return Type**: `void`
- **Calls**:
  - `checkDuplicate`
  - `isFunctionOrFunctionType (from ../util)`
  - `maybeFunction.params.includes`
  - `tsutils.isTypeFlagSet`
  - `report`

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
    ignoreIntersections?: boolean;
    ignoreUnions?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'duplicate' | 'unnecessary';
```

### `UnionOrIntersection`

```ts
type UnionOrIntersection = 'Intersection' | 'Union';
```


---