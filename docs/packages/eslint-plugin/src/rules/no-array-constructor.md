[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-array-constructor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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
📂 **`packages/eslint-plugin/src/rules/no-array-constructor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `isOpeningParenToken` | `@typescript-eslint/utils/ast-utils` |
| `isClosingParenToken` | `@typescript-eslint/utils/ast-utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `sourceCode` | `any` | const | `context.sourceCode` | ✗ |
| `firstToken` | `TSESTree.Expression | TSESTree.Token | null` | let/var | `node.callee` | ✗ |


---

## Functions

### `getArgumentsText(node: TSESTree.CallExpression | TSESTree.NewExpression): any`

<details><summary>Code</summary>

```ts
function getArgumentsText(
      node: TSESTree.CallExpression | TSESTree.NewExpression,
    ) {
      const lastToken = sourceCode.getLastToken(node);

      if (lastToken == null || !isClosingParenToken(lastToken)) {
        return '';
      }

      let firstToken: TSESTree.Expression | TSESTree.Token | null = node.callee;

      do {
        firstToken = sourceCode.getTokenAfter(firstToken);
        if (!firstToken || firstToken === lastToken) {
          return '';
        }
      } while (!isOpeningParenToken(firstToken));

      return sourceCode.text.slice(firstToken.range[1], lastToken.range[0]);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.NewExpression`
- **Return Type**: `any`
- **Calls**:
  - `sourceCode.getLastToken`
  - `isClosingParenToken (from @typescript-eslint/utils/ast-utils)`
  - `sourceCode.getTokenAfter`
  - `isOpeningParenToken (from @typescript-eslint/utils/ast-utils)`
  - `sourceCode.text.slice`
### `check(node: TSESTree.CallExpression | TSESTree.NewExpression): void`

<details><summary>Code</summary>

```ts
function check(
      node: TSESTree.CallExpression | TSESTree.NewExpression,
    ): void {
      if (
        node.arguments.length !== 1 &&
        node.callee.type === AST_NODE_TYPES.Identifier &&
        node.callee.name === 'Array' &&
        !node.typeArguments
      ) {
        context.report({
          node,
          messageId: 'useLiteral',
          fix(fixer) {
            const argsText = getArgumentsText(node);

            return fixer.replaceText(node, `[${argsText}]`);
          },
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Disallow construction of dense arrays using the Array constructor
     * @param node node to evaluate
     */
```

- **Parameters**:
  - `node: TSESTree.CallExpression | TSESTree.NewExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getArgumentsText`
  - `fixer.replaceText`

---