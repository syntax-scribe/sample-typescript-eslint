[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-assertions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 15 |
| 🧱 Classes | 0 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 4 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-type-assertions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getOperatorPrecedence` | `../util` |
| `getOperatorPrecedenceForNode` | `../util` |
| `getParserServices` | `../util` |
| `getTextWithParentheses` | `../util` |
| `isParenthesized` | `../util` |
| `getWrappedCode` | `../util/getWrappedCode` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `messageId` | `any` | const | `options.assertionStyle` | ✗ |
| `text` | `string` | const | ``${expressionCodeWrapped} as ${typeAnnotationCode}`` | ✗ |
| `suggestions` | `TSESLint.ReportSuggestionArray<MessageIds>` | const | `[]` | ✗ |


---

## Functions

### `isConst(node: TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function isConst(node: TSESTree.TypeNode): boolean {
      if (node.type !== AST_NODE_TYPES.TSTypeReference) {
        return false;
      }

      return (
        node.typeName.type === AST_NODE_TYPES.Identifier &&
        node.typeName.name === 'const'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TypeNode`
- **Return Type**: `boolean`
### `reportIncorrectAssertionType(node: AsExpressionOrTypeAssertion): void`

<details><summary>Code</summary>

```ts
function reportIncorrectAssertionType(
      node: AsExpressionOrTypeAssertion,
    ): void {
      const messageId = options.assertionStyle;

      // If this node is `as const`, then don't report an error.
      if (isConst(node.typeAnnotation) && messageId === 'never') {
        return;
      }
      context.report({
        node,
        messageId,
        data:
          messageId !== 'never'
            ? { cast: context.sourceCode.getText(node.typeAnnotation) }
            : {},
        fix:
          messageId === 'as'
            ? (fixer): TSESLint.RuleFix => {
                // lazily access parserServices to avoid crashing on non TS files (#9860)
                const tsNode = getParserServices(
                  context,
                  true,
                ).esTreeNodeToTSNodeMap.get(node as TSESTree.TSTypeAssertion);

                const expressionCode = context.sourceCode.getText(
                  node.expression,
                );
                const typeAnnotationCode = context.sourceCode.getText(
                  node.typeAnnotation,
                );

                const asPrecedence = getOperatorPrecedence(
                  ts.SyntaxKind.AsExpression,
                  ts.SyntaxKind.Unknown,
                );
                const parentPrecedence = getOperatorPrecedence(
                  tsNode.parent.kind,
                  ts.isBinaryExpression(tsNode.parent)
                    ? tsNode.parent.operatorToken.kind
                    : ts.SyntaxKind.Unknown,
                  ts.isNewExpression(tsNode.parent)
                    ? tsNode.parent.arguments != null &&
                        tsNode.parent.arguments.length > 0
                    : undefined,
                );

                const expressionPrecedence = getOperatorPrecedenceForNode(
                  node.expression,
                );

                const expressionCodeWrapped = getWrappedCode(
                  expressionCode,
                  expressionPrecedence,
                  asPrecedence,
                );

                const text = `${expressionCodeWrapped} as ${typeAnnotationCode}`;
                return fixer.replaceText(
                  node,
                  isParenthesized(node, context.sourceCode)
                    ? text
                    : getWrappedCode(text, asPrecedence, parentPrecedence),
                );
              }
            : undefined,
      });
    }
```
</details>

- **Parameters**:
  - `node: AsExpressionOrTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `isConst`
  - `context.report`
  - `context.sourceCode.getText`
  - `getParserServices(
                  context,
                  true,
                ).esTreeNodeToTSNodeMap.get`
  - `getOperatorPrecedence (from ../util)`
  - `ts.isBinaryExpression`
  - `ts.isNewExpression`
  - `getOperatorPrecedenceForNode (from ../util)`
  - `getWrappedCode (from ../util/getWrappedCode)`
  - `fixer.replaceText`
  - `isParenthesized (from ../util)`
- **Internal Comments**:
```
// If this node is `as const`, then don't report an error.
// lazily access parserServices to avoid crashing on non TS files (#9860) (x2)
```

### `checkType(node: TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function checkType(node: TSESTree.TypeNode): boolean {
      switch (node.type) {
        case AST_NODE_TYPES.TSAnyKeyword:
        case AST_NODE_TYPES.TSUnknownKeyword:
          return false;
        case AST_NODE_TYPES.TSTypeReference:
          return (
            // Ignore `as const` and `<const>`
            !isConst(node) ||
            // Allow qualified names which have dots between identifiers, `Foo.Bar`
            node.typeName.type === AST_NODE_TYPES.TSQualifiedName
          );

        default:
          return true;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TypeNode`
- **Return Type**: `boolean`
- **Calls**:
  - `isConst`
- **Internal Comments**:
```
// Ignore `as const` and `<const>` (x2)
// Allow qualified names which have dots between identifiers, `Foo.Bar` (x4)
```

### `getSuggestions(node: AsExpressionOrTypeAssertion, annotationMessageId: MessageIds, satisfiesMessageId: MessageIds): TSESLint.ReportSuggestionArray<MessageIds>`

<details><summary>Code</summary>

```ts
function getSuggestions(
      node: AsExpressionOrTypeAssertion,
      annotationMessageId: MessageIds,
      satisfiesMessageId: MessageIds,
    ): TSESLint.ReportSuggestionArray<MessageIds> {
      const suggestions: TSESLint.ReportSuggestionArray<MessageIds> = [];
      if (
        node.parent.type === AST_NODE_TYPES.VariableDeclarator &&
        !node.parent.id.typeAnnotation
      ) {
        const { parent } = node;
        suggestions.push({
          messageId: annotationMessageId,
          data: { cast: context.sourceCode.getText(node.typeAnnotation) },
          fix: fixer => [
            fixer.insertTextAfter(
              parent.id,
              `: ${context.sourceCode.getText(node.typeAnnotation)}`,
            ),
            fixer.replaceText(
              node,
              getTextWithParentheses(context.sourceCode, node.expression),
            ),
          ],
        });
      }
      suggestions.push({
        messageId: satisfiesMessageId,
        data: { cast: context.sourceCode.getText(node.typeAnnotation) },
        fix: fixer => [
          fixer.replaceText(
            node,
            getTextWithParentheses(context.sourceCode, node.expression),
          ),
          fixer.insertTextAfter(
            node,
            ` satisfies ${context.sourceCode.getText(node.typeAnnotation)}`,
          ),
        ],
      });
      return suggestions;
    }
```
</details>

- **Parameters**:
  - `node: AsExpressionOrTypeAssertion`
  - `annotationMessageId: MessageIds`
  - `satisfiesMessageId: MessageIds`
- **Return Type**: `TSESLint.ReportSuggestionArray<MessageIds>`
- **Calls**:
  - `suggestions.push`
  - `context.sourceCode.getText`
  - `fixer.insertTextAfter`
  - `fixer.replaceText`
  - `getTextWithParentheses (from ../util)`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
            fixer.insertTextAfter(
              parent.id,
              `: ${context.sourceCode.getText(node.typeAnnotation)}`,
            ),
            fixer.replaceText(
              node,
              getTextWithParentheses(context.sourceCode, node.expression),
            ),
          ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
            fixer.insertTextAfter(
              parent.id,
              `: ${context.sourceCode.getText(node.typeAnnotation)}`,
            ),
            fixer.replaceText(
              node,
              getTextWithParentheses(context.sourceCode, node.expression),
            ),
          ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
          fixer.replaceText(
            node,
            getTextWithParentheses(context.sourceCode, node.expression),
          ),
          fixer.insertTextAfter(
            node,
            ` satisfies ${context.sourceCode.getText(node.typeAnnotation)}`,
          ),
        ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
          fixer.replaceText(
            node,
            getTextWithParentheses(context.sourceCode, node.expression),
          ),
          fixer.insertTextAfter(
            node,
            ` satisfies ${context.sourceCode.getText(node.typeAnnotation)}`,
          ),
        ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `isAsParameter(node: AsExpressionOrTypeAssertion): boolean`

<details><summary>Code</summary>

```ts
function isAsParameter(node: AsExpressionOrTypeAssertion): boolean {
      return (
        node.parent.type === AST_NODE_TYPES.NewExpression ||
        node.parent.type === AST_NODE_TYPES.CallExpression ||
        node.parent.type === AST_NODE_TYPES.ThrowStatement ||
        node.parent.type === AST_NODE_TYPES.AssignmentPattern ||
        node.parent.type === AST_NODE_TYPES.JSXExpressionContainer ||
        (node.parent.type === AST_NODE_TYPES.TemplateLiteral &&
          node.parent.parent.type === AST_NODE_TYPES.TaggedTemplateExpression)
      );
    }
```
</details>

- **Parameters**:
  - `node: AsExpressionOrTypeAssertion`
- **Return Type**: `boolean`
### `checkExpressionForObjectAssertion(node: AsExpressionOrTypeAssertion): void`

<details><summary>Code</summary>

```ts
function checkExpressionForObjectAssertion(
      node: AsExpressionOrTypeAssertion,
    ): void {
      if (
        options.assertionStyle === 'never' ||
        options.objectLiteralTypeAssertions === 'allow' ||
        node.expression.type !== AST_NODE_TYPES.ObjectExpression
      ) {
        return;
      }

      if (
        options.objectLiteralTypeAssertions === 'allow-as-parameter' &&
        isAsParameter(node)
      ) {
        return;
      }

      if (checkType(node.typeAnnotation)) {
        const suggest = getSuggestions(
          node,
          'replaceObjectTypeAssertionWithAnnotation',
          'replaceObjectTypeAssertionWithSatisfies',
        );

        context.report({
          node,
          messageId: 'unexpectedObjectTypeAssertion',
          suggest,
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: AsExpressionOrTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `isAsParameter`
  - `checkType`
  - `getSuggestions`
  - `context.report`
### `checkExpressionForArrayAssertion(node: AsExpressionOrTypeAssertion): void`

<details><summary>Code</summary>

```ts
function checkExpressionForArrayAssertion(
      node: AsExpressionOrTypeAssertion,
    ): void {
      if (
        options.assertionStyle === 'never' ||
        options.arrayLiteralTypeAssertions === 'allow' ||
        node.expression.type !== AST_NODE_TYPES.ArrayExpression
      ) {
        return;
      }

      if (
        options.arrayLiteralTypeAssertions === 'allow-as-parameter' &&
        isAsParameter(node)
      ) {
        return;
      }

      if (checkType(node.typeAnnotation)) {
        const suggest = getSuggestions(
          node,
          'replaceArrayTypeAssertionWithAnnotation',
          'replaceArrayTypeAssertionWithSatisfies',
        );

        context.report({
          node,
          messageId: 'unexpectedArrayTypeAssertion',
          suggest,
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: AsExpressionOrTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `isAsParameter`
  - `checkType`
  - `getSuggestions`
  - `context.report`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
            fixer.insertTextAfter(
              parent.id,
              `: ${context.sourceCode.getText(node.typeAnnotation)}`,
            ),
            fixer.replaceText(
              node,
              getTextWithParentheses(context.sourceCode, node.expression),
            ),
          ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
            fixer.insertTextAfter(
              parent.id,
              `: ${context.sourceCode.getText(node.typeAnnotation)}`,
            ),
            fixer.replaceText(
              node,
              getTextWithParentheses(context.sourceCode, node.expression),
            ),
          ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
          fixer.replaceText(
            node,
            getTextWithParentheses(context.sourceCode, node.expression),
          ),
          fixer.insertTextAfter(
            node,
            ` satisfies ${context.sourceCode.getText(node.typeAnnotation)}`,
          ),
        ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
          fixer.replaceText(
            node,
            getTextWithParentheses(context.sourceCode, node.expression),
          ),
          fixer.insertTextAfter(
            node,
            ` satisfies ${context.sourceCode.getText(node.typeAnnotation)}`,
          ),
        ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'angle-bracket'
  | 'as'
  | 'never'
  | 'replaceArrayTypeAssertionWithAnnotation'
  | 'replaceArrayTypeAssertionWithSatisfies'
  | 'replaceObjectTypeAssertionWithAnnotation'
  | 'replaceObjectTypeAssertionWithSatisfies'
  | 'unexpectedArrayTypeAssertion'
  | 'unexpectedObjectTypeAssertion';
```

### `OptUnion`

```ts
type OptUnion = | {
      assertionStyle: 'angle-bracket' | 'as';
      objectLiteralTypeAssertions?: 'allow' | 'allow-as-parameter' | 'never';
      arrayLiteralTypeAssertions?: 'allow' | 'allow-as-parameter' | 'never';
    }
  | {
      assertionStyle: 'never';
    };
```

### `Options`

```ts
type Options = readonly [OptUnion];
```

### `AsExpressionOrTypeAssertion`

```ts
type AsExpressionOrTypeAssertion = | TSESTree.TSAsExpression
  | TSESTree.TSTypeAssertion;
```


---