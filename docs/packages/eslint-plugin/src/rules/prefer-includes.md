[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-includes.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 7 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 14 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-includes.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `parseRegExpLiteral` | `@eslint-community/regexpp` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getStaticValue` | `../util` |
| `isStaticMemberAccessOfValue` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `paramsA` | `any` | const | `nodeA.parameters` | ✗ |
| `paramsB` | `any` | const | `nodeB.parameters` | ✗ |
| `paramA` | `any` | const | `paramsA[i]` | ✗ |
| `paramB` | `any` | const | `paramsB[i]` | ✗ |
| `chars` | `any` | const | `pattern.alternatives[0].elements` | ✗ |
| `EscapeMap` | `{ '\0': string; '\t': string; '\n': string; '\v': string; '\f': string; '\r': string; "'": string; '\\': string; }` | const | `{
        '\0': '\\0',
        '\t': '\\t',
        '\n': '\\n',
        '\v': '\\v',
        '\f': '\\f',
        '\r': '\\r',
        "'": "\\'",
        '\\': '\\\\',
        // "\b" cause unexpected replacements
        // '\b': '\\b',
      }` | ✗ |
| `replaceRegex` | `RegExp` | const | `new RegExp(Object.values(EscapeMap).join('|'), 'g')` | ✗ |
| `callNode` | `TSESTree.CallExpression` | const | `node.parent as TSESTree.CallExpression` | ✗ |
| `compareNode` | `TSESTree.BinaryExpression` | const | `(
        callNode.parent.type === AST_NODE_TYPES.ChainExpression
          ? callNode.parent.parent
          : callNode.parent
      ) as TSESTree.BinaryExpression` | ✗ |
| `typeDecl` | `any` | const | `instanceofMethodDecl.parent` | ✗ |
| `callNode` | `any` | const | `node.parent` | ✗ |
| `argument` | `any` | const | `callNode.arguments[0]` | ✗ |
| `argNode` | `any` | let/var | `callNode.arguments[0]` | ✗ |
| `needsParen` | `boolean` | let/var | `argNode.type !== AST_NODE_TYPES.Literal &&
              argNode.type !== AST_NODE_TYPES.TemplateLiteral &&
              argNode.type !== AST_NODE_TYPES.Identifier &&
              argNode.type !== AST_NODE_TYPES.MemberExpression &&
              argNode.type !== AST_NODE_TYPES.CallExpression` | ✗ |


---

## Functions

### `isNumber(node: TSESTree.Node, value: number): boolean`

<details><summary>Code</summary>

```ts
function isNumber(node: TSESTree.Node, value: number): boolean {
      const evaluated = getStaticValue(node, globalScope);
      return evaluated != null && evaluated.value === value;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `value: number`
- **Return Type**: `boolean`
- **Calls**:
  - `getStaticValue (from ../util)`
### `isPositiveCheck(node: TSESTree.BinaryExpression): boolean`

<details><summary>Code</summary>

```ts
function isPositiveCheck(node: TSESTree.BinaryExpression): boolean {
      switch (node.operator) {
        case '!==':
        case '!=':
        case '>':
          return isNumber(node.right, -1);
        case '>=':
          return isNumber(node.right, 0);
        default:
          return false;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.BinaryExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isNumber`
### `isNegativeCheck(node: TSESTree.BinaryExpression): boolean`

<details><summary>Code</summary>

```ts
function isNegativeCheck(node: TSESTree.BinaryExpression): boolean {
      switch (node.operator) {
        case '===':
        case '==':
        case '<=':
          return isNumber(node.right, -1);
        case '<':
          return isNumber(node.right, 0);
        default:
          return false;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.BinaryExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isNumber`
### `hasSameParameters(nodeA: ts.Declaration, nodeB: ts.Declaration): boolean`

<details><summary>Code</summary>

```ts
function hasSameParameters(
      nodeA: ts.Declaration,
      nodeB: ts.Declaration,
    ): boolean {
      if (!ts.isFunctionLike(nodeA) || !ts.isFunctionLike(nodeB)) {
        return false;
      }

      const paramsA = nodeA.parameters;
      const paramsB = nodeB.parameters;
      if (paramsA.length !== paramsB.length) {
        return false;
      }

      for (let i = 0; i < paramsA.length; ++i) {
        const paramA = paramsA[i];
        const paramB = paramsB[i];

        // Check name, type, and question token once.
        if (paramA.getText() !== paramB.getText()) {
          return false;
        }
      }

      return true;
    }
```
</details>

- **Parameters**:
  - `nodeA: ts.Declaration`
  - `nodeB: ts.Declaration`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isFunctionLike`
  - `paramA.getText`
  - `paramB.getText`
- **Internal Comments**:
```
// Check name, type, and question token once.
```

### `parseRegExp(node: TSESTree.Node): string | null`

<details><summary>Code</summary>

```ts
function parseRegExp(node: TSESTree.Node): string | null {
      const evaluated = getStaticValue(node, globalScope);
      if (evaluated == null || !(evaluated.value instanceof RegExp)) {
        return null;
      }

      const { flags, pattern } = parseRegExpLiteral(evaluated.value);
      if (
        pattern.alternatives.length !== 1 ||
        flags.ignoreCase ||
        flags.global
      ) {
        return null;
      }

      // Check if it can determine a unique string.
      const chars = pattern.alternatives[0].elements;
      if (!chars.every(c => c.type === 'Character')) {
        return null;
      }

      // To string.
      return String.fromCodePoint(...chars.map(c => c.value));
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Parse a given node if it's a `RegExp` instance.
     * @param node The node to parse.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `string | null`
- **Calls**:
  - `getStaticValue (from ../util)`
  - `parseRegExpLiteral (from @eslint-community/regexpp)`
  - `chars.every`
  - `String.fromCodePoint`
  - `chars.map`
- **Internal Comments**:
```
// Check if it can determine a unique string. (x2)
// To string.
```

### `escapeString(str: string): string`

<details><summary>Code</summary>

```ts
function escapeString(str: string): string {
      const EscapeMap = {
        '\0': '\\0',
        '\t': '\\t',
        '\n': '\\n',
        '\v': '\\v',
        '\f': '\\f',
        '\r': '\\r',
        "'": "\\'",
        '\\': '\\\\',
        // "\b" cause unexpected replacements
        // '\b': '\\b',
      };
      const replaceRegex = new RegExp(Object.values(EscapeMap).join('|'), 'g');

      return str.replaceAll(
        replaceRegex,
        char => EscapeMap[char as keyof typeof EscapeMap],
      );
    }
```
</details>

- **Parameters**:
  - `str: string`
- **Return Type**: `string`
- **Calls**:
  - `Object.values(EscapeMap).join`
  - `str.replaceAll`
### `checkArrayIndexOf(node: TSESTree.MemberExpression, allowFixing: boolean): void`

<details><summary>Code</summary>

```ts
function checkArrayIndexOf(
      node: TSESTree.MemberExpression,
      allowFixing: boolean,
    ): void {
      if (!isStaticMemberAccessOfValue(node, context, 'indexOf')) {
        return;
      }
      // Check if the comparison is equivalent to `includes()`.
      const callNode = node.parent as TSESTree.CallExpression;
      const compareNode = (
        callNode.parent.type === AST_NODE_TYPES.ChainExpression
          ? callNode.parent.parent
          : callNode.parent
      ) as TSESTree.BinaryExpression;
      const negative = isNegativeCheck(compareNode);
      if (!negative && !isPositiveCheck(compareNode)) {
        return;
      }

      // Get the symbol of `indexOf` method.
      const indexofMethodDeclarations = services
        .getSymbolAtLocation(node.property)
        ?.getDeclarations();
      if (
        indexofMethodDeclarations == null ||
        indexofMethodDeclarations.length === 0
      ) {
        return;
      }

      // Check if every declaration of `indexOf` method has `includes` method
      // and the two methods have the same parameters.
      for (const instanceofMethodDecl of indexofMethodDeclarations) {
        const typeDecl = instanceofMethodDecl.parent;
        const type = checker.getTypeAtLocation(typeDecl);
        const includesMethodDecl = type
          .getProperty('includes')
          ?.getDeclarations();
        if (
          !includesMethodDecl?.some(includesMethodDecl =>
            hasSameParameters(includesMethodDecl, instanceofMethodDecl),
          )
        ) {
          return;
        }
      }

      // Report it.
      context.report({
        node: compareNode,
        messageId: 'preferIncludes',
        ...(allowFixing && {
          *fix(fixer): Generator<TSESLint.RuleFix> {
            if (negative) {
              yield fixer.insertTextBefore(callNode, '!');
            }
            yield fixer.replaceText(node.property, 'includes');
            yield fixer.removeRange([callNode.range[1], compareNode.range[1]]);
          },
        }),
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
  - `allowFixing: boolean`
- **Return Type**: `void`
- **Calls**:
  - `isStaticMemberAccessOfValue (from ../util)`
  - `isNegativeCheck`
  - `isPositiveCheck`
  - `services
        .getSymbolAtLocation(node.property)
        ?.getDeclarations`
  - `checker.getTypeAtLocation`
  - `type
          .getProperty('includes')
          ?.getDeclarations`
  - `includesMethodDecl?.some`
  - `hasSameParameters`
  - `context.report`
  - `fixer.insertTextBefore`
  - `fixer.replaceText`
  - `fixer.removeRange`
- **Internal Comments**:
```
// Check if the comparison is equivalent to `includes()`. (x2)
// Get the symbol of `indexOf` method. (x2)
// Check if every declaration of `indexOf` method has `includes` method
// and the two methods have the same parameters.
// Report it. (x4)
```


---