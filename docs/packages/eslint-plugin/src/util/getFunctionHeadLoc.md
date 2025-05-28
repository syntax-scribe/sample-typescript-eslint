[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getFunctionHeadLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getFunctionHeadLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `isArrowToken` | `./astUtils` |
| `isOpeningParenToken` | `./astUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parent` | `any` | const | `node.parent` | ✗ |
| `start` | `TSESTree.Position | null` | let/var | `null` | ✗ |
| `end` | `TSESTree.Position | null` | let/var | `null` | ✗ |
| `lastDecorator` | `any` | const | `parent.decorators[parent.decorators.length - 1]` | ✗ |


---

## Functions

### `getOpeningParenOfParams(node: FunctionNode, sourceCode: TSESLint.SourceCode): TSESTree.Token`

<details><summary>Code</summary>

```ts
function getOpeningParenOfParams(
  node: FunctionNode,
  sourceCode: TSESLint.SourceCode,
): TSESTree.Token {
  // If the node is an arrow function and doesn't have parens, this returns the identifier of the first param.
  if (
    node.type === AST_NODE_TYPES.ArrowFunctionExpression &&
    node.params.length === 1
  ) {
    const argToken = ESLintUtils.nullThrows(
      sourceCode.getFirstToken(node.params[0]),
      ESLintUtils.NullThrowsReasons.MissingToken('parameter', 'arrow function'),
    );
    const maybeParenToken = sourceCode.getTokenBefore(argToken);

    return maybeParenToken && isOpeningParenToken(maybeParenToken)
      ? maybeParenToken
      : argToken;
  }

  // Otherwise, returns paren.
  return node.id != null
    ? ESLintUtils.nullThrows(
        sourceCode.getTokenAfter(node.id, isOpeningParenToken),
        ESLintUtils.NullThrowsReasons.MissingToken('id', 'function'),
      )
    : ESLintUtils.nullThrows(
        sourceCode.getFirstToken(node, isOpeningParenToken),
        ESLintUtils.NullThrowsReasons.MissingToken(
          'opening parenthesis',
          'function',
        ),
      );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the `(` token of the given function node.
 * @param node The function node to get.
 * @param sourceCode The source code object to get tokens.
 * @returns `(` token.
 */
```

- **Parameters**:
  - `node: FunctionNode`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `TSESTree.Token`
- **Calls**:
  - `ESLintUtils.nullThrows`
  - `sourceCode.getFirstToken`
  - `ESLintUtils.NullThrowsReasons.MissingToken`
  - `sourceCode.getTokenBefore`
  - `isOpeningParenToken (from ./astUtils)`
  - `sourceCode.getTokenAfter`
- **Internal Comments**:
```
// If the node is an arrow function and doesn't have parens, this returns the identifier of the first param.
// Otherwise, returns paren.
```

### `getFunctionHeadLoc(node: FunctionNode, sourceCode: TSESLint.SourceCode): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getFunctionHeadLoc(
  node: FunctionNode,
  sourceCode: TSESLint.SourceCode,
): TSESTree.SourceLocation {
  const parent = node.parent;
  let start: TSESTree.Position | null = null;
  let end: TSESTree.Position | null = null;

  if (
    parent.type === AST_NODE_TYPES.MethodDefinition ||
    parent.type === AST_NODE_TYPES.PropertyDefinition
  ) {
    // the decorator's range is included within the member
    // however it's usually irrelevant to the member itself - so we don't want
    // to highlight it ever.
    if (parent.decorators.length > 0) {
      const lastDecorator = parent.decorators[parent.decorators.length - 1];
      const firstTokenAfterDecorator = ESLintUtils.nullThrows(
        sourceCode.getTokenAfter(lastDecorator),
        ESLintUtils.NullThrowsReasons.MissingToken(
          'modifier or member name',
          'class member',
        ),
      );
      start = firstTokenAfterDecorator.loc.start;
    } else {
      start = parent.loc.start;
    }
    end = getOpeningParenOfParams(node, sourceCode).loc.start;
  } else if (parent.type === AST_NODE_TYPES.Property) {
    start = parent.loc.start;
    end = getOpeningParenOfParams(node, sourceCode).loc.start;
  } else if (node.type === AST_NODE_TYPES.ArrowFunctionExpression) {
    const arrowToken = ESLintUtils.nullThrows(
      sourceCode.getTokenBefore(node.body, isArrowToken),
      ESLintUtils.NullThrowsReasons.MissingToken(
        'arrow token',
        'arrow function',
      ),
    );

    start = arrowToken.loc.start;
    end = arrowToken.loc.end;
  } else {
    start = node.loc.start;
    end = getOpeningParenOfParams(node, sourceCode).loc.start;
  }

  return {
    end: { ...end },
    start: { ...start },
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the location of the given function node for reporting.
 *
 * - `function foo() {}`
 *    ^^^^^^^^^^^^
 * - `(function foo() {})`
 *     ^^^^^^^^^^^^
 * - `(function() {})`
 *     ^^^^^^^^
 * - `function* foo() {}`
 *    ^^^^^^^^^^^^^
 * - `(function* foo() {})`
 *     ^^^^^^^^^^^^^
 * - `(function*() {})`
 *     ^^^^^^^^^
 * - `() => {}`
 *       ^^
 * - `async () => {}`
 *             ^^
 * - `({ foo: function foo() {} })`
 *       ^^^^^^^^^^^^^^^^^
 * - `({ foo: function() {} })`
 *       ^^^^^^^^^^^^^
 * - `({ ['foo']: function() {} })`
 *       ^^^^^^^^^^^^^^^^^
 * - `({ [foo]: function() {} })`
 *       ^^^^^^^^^^^^^^^
 * - `({ foo() {} })`
 *       ^^^
 * - `({ foo: function* foo() {} })`
 *       ^^^^^^^^^^^^^^^^^^
 * - `({ foo: function*() {} })`
 *       ^^^^^^^^^^^^^^
 * - `({ ['foo']: function*() {} })`
 *       ^^^^^^^^^^^^^^^^^^
 * - `({ [foo]: function*() {} })`
 *       ^^^^^^^^^^^^^^^^
 * - `({ *foo() {} })`
 *       ^^^^
 * - `({ foo: async function foo() {} })`
 *       ^^^^^^^^^^^^^^^^^^^^^^^
 * - `({ foo: async function() {} })`
 *       ^^^^^^^^^^^^^^^^^^^
 * - `({ ['foo']: async function() {} })`
 *       ^^^^^^^^^^^^^^^^^^^^^^^
 * - `({ [foo]: async function() {} })`
 *       ^^^^^^^^^^^^^^^^^^^^^
 * - `({ async foo() {} })`
 *       ^^^^^^^^^
 * - `({ get foo() {} })`
 *       ^^^^^^^
 * - `({ set foo(a) {} })`
 *       ^^^^^^^
 * - `class A { constructor() {} }`
 *              ^^^^^^^^^^^
 * - `class A { foo() {} }`
 *              ^^^
 * - `class A { *foo() {} }`
 *              ^^^^
 * - `class A { async foo() {} }`
 *              ^^^^^^^^^
 * - `class A { ['foo']() {} }`
 *              ^^^^^^^
 * - `class A { *['foo']() {} }`
 *              ^^^^^^^^
 * - `class A { async ['foo']() {} }`
 *              ^^^^^^^^^^^^^
 * - `class A { [foo]() {} }`
 *              ^^^^^
 * - `class A { *[foo]() {} }`
 *              ^^^^^^
 * - `class A { async [foo]() {} }`
 *              ^^^^^^^^^^^
 * - `class A { get foo() {} }`
 *              ^^^^^^^
 * - `class A { set foo(a) {} }`
 *              ^^^^^^^
 * - `class A { static foo() {} }`
 *              ^^^^^^^^^^
 * - `class A { static *foo() {} }`
 *              ^^^^^^^^^^^
 * - `class A { static async foo() {} }`
 *              ^^^^^^^^^^^^^^^^
 * - `class A { static get foo() {} }`
 *              ^^^^^^^^^^^^^^
 * - `class A { static set foo(a) {} }`
 *              ^^^^^^^^^^^^^^
 * - `class A { foo = function() {} }`
 *              ^^^^^^^^^^^^^^
 * - `class A { static foo = function() {} }`
 *              ^^^^^^^^^^^^^^^^^^^^^
 * - `class A { foo = (a, b) => {} }`
 *              ^^^^^^
 * @param node The function node to get.
 * @param sourceCode The source code object to get tokens.
 * @returns The location of the function node for reporting.
 */
```

- **Parameters**:
  - `node: FunctionNode`
  - `sourceCode: TSESLint.SourceCode`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `ESLintUtils.nullThrows`
  - `sourceCode.getTokenAfter`
  - `ESLintUtils.NullThrowsReasons.MissingToken`
  - `getOpeningParenOfParams`
  - `sourceCode.getTokenBefore`
- **Internal Comments**:
```
// the decorator's range is included within the member
// however it's usually irrelevant to the member itself - so we don't want
// to highlight it ever.
```


---

## Type Aliases

### `FunctionNode`

```ts
type FunctionNode = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression;
```


---