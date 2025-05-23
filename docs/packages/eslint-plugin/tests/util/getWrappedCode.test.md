[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappedCode.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/util/getWrappedCode.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `createRule` | `../../src/util` |
| `getOperatorPrecedence` | `../../src/util` |
| `getParserServices` | `../../src/util` |
| `getWrappedCode` | `../../src/util/getWrappedCode` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Functions

### `report(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.CallExpression): void => {
      context.report({
        fix: fixer => {
          const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const tsArgumentNode = tsNode.arguments[0];

          const nodePrecedence = getOperatorPrecedence(
            tsArgumentNode.kind,
            ts.isBinaryExpression(tsArgumentNode)
              ? tsArgumentNode.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );
          const parentPrecedence = getOperatorPrecedence(
            tsNode.parent.kind,
            ts.isBinaryExpression(tsNode.parent)
              ? tsNode.parent.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );

          const text = context.sourceCode.getText(node.arguments[0]);
          return fixer.replaceText(
            node,
            getWrappedCode(text, nodePrecedence, parentPrecedence),
          );
        },
        messageId: 'removeFunction',
        node,
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../../src/util)`
  - `ts.isBinaryExpression`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
  - `getWrappedCode (from ../../src/util/getWrappedCode)`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
          const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const tsArgumentNode = tsNode.arguments[0];

          const nodePrecedence = getOperatorPrecedence(
            tsArgumentNode.kind,
            ts.isBinaryExpression(tsArgumentNode)
              ? tsArgumentNode.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );
          const parentPrecedence = getOperatorPrecedence(
            tsNode.parent.kind,
            ts.isBinaryExpression(tsNode.parent)
              ? tsNode.parent.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );

          const text = context.sourceCode.getText(node.arguments[0]);
          return fixer.replaceText(
            node,
            getWrappedCode(text, nodePrecedence, parentPrecedence),
          );
        }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../../src/util)`
  - `ts.isBinaryExpression`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
  - `getWrappedCode (from ../../src/util/getWrappedCode)`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
          const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const tsArgumentNode = tsNode.arguments[0];

          const nodePrecedence = getOperatorPrecedence(
            tsArgumentNode.kind,
            ts.isBinaryExpression(tsArgumentNode)
              ? tsArgumentNode.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );
          const parentPrecedence = getOperatorPrecedence(
            tsNode.parent.kind,
            ts.isBinaryExpression(tsNode.parent)
              ? tsNode.parent.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );

          const text = context.sourceCode.getText(node.arguments[0]);
          return fixer.replaceText(
            node,
            getWrappedCode(text, nodePrecedence, parentPrecedence),
          );
        }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../../src/util)`
  - `ts.isBinaryExpression`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
  - `getWrappedCode (from ../../src/util/getWrappedCode)`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
          const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const tsArgumentNode = tsNode.arguments[0];

          const nodePrecedence = getOperatorPrecedence(
            tsArgumentNode.kind,
            ts.isBinaryExpression(tsArgumentNode)
              ? tsArgumentNode.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );
          const parentPrecedence = getOperatorPrecedence(
            tsNode.parent.kind,
            ts.isBinaryExpression(tsNode.parent)
              ? tsNode.parent.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );

          const text = context.sourceCode.getText(node.arguments[0]);
          return fixer.replaceText(
            node,
            getWrappedCode(text, nodePrecedence, parentPrecedence),
          );
        }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../../src/util)`
  - `ts.isBinaryExpression`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
  - `getWrappedCode (from ../../src/util/getWrappedCode)`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
          const tsNode = parserServices.esTreeNodeToTSNodeMap.get(node);
          const tsArgumentNode = tsNode.arguments[0];

          const nodePrecedence = getOperatorPrecedence(
            tsArgumentNode.kind,
            ts.isBinaryExpression(tsArgumentNode)
              ? tsArgumentNode.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );
          const parentPrecedence = getOperatorPrecedence(
            tsNode.parent.kind,
            ts.isBinaryExpression(tsNode.parent)
              ? tsNode.parent.operatorToken.kind
              : ts.SyntaxKind.Unknown,
          );

          const text = context.sourceCode.getText(node.arguments[0]);
          return fixer.replaceText(
            node,
            getWrappedCode(text, nodePrecedence, parentPrecedence),
          );
        }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `parserServices.esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../../src/util)`
  - `ts.isBinaryExpression`
  - `context.sourceCode.getText`
  - `fixer.replaceText`
  - `getWrappedCode (from ../../src/util/getWrappedCode)`

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