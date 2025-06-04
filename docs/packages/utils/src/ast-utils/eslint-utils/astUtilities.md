[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `astUtilities.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📊 Variables & Constants | 7 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/eslint-utils/astUtilities.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../ts-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `getFunctionHeadLocation` | `(node: any, sourceCode: SourceCode) => TSESTree.SourceLocation` | const | `eslintUtils.getFunctionHeadLocation as (
  node:
    | TSESTree.ArrowFunctionExpression
    | TSESTree.FunctionDeclaration
    | TSESTree.FunctionExpression,
  sourceCode: TSESLint.SourceCode,
) => TSESTree.SourceLocation` | ✓ |
| `getFunctionNameWithKind` | `(node: any, sourceCode?: SourceCode) => string` | const | `eslintUtils.getFunctionNameWithKind as (
  node:
    | TSESTree.ArrowFunctionExpression
    | TSESTree.FunctionDeclaration
    | TSESTree.FunctionExpression,
  sourceCode?: TSESLint.SourceCode,
) => string` | ✓ |
| `getPropertyName` | `(node: any, initialScope?: scopeManager.Scope) => string` | const | `eslintUtils.getPropertyName as (
  node:
    | TSESTree.MemberExpression
    | TSESTree.MethodDefinition
    | TSESTree.Property
    | TSESTree.PropertyDefinition,
  initialScope?: TSESLint.Scope.Scope,
) => string | null` | ✓ |
| `getStaticValue` | `(node: TSESTree.Node, initialScope?: scopeManager.Scope) => { value: unknown; }` | const | `eslintUtils.getStaticValue as (
  node: TSESTree.Node,
  initialScope?: TSESLint.Scope.Scope,
) => { value: unknown } | null` | ✓ |
| `getStringIfConstant` | `(node: TSESTree.Node, initialScope?: scopeManager.Scope) => string` | const | `eslintUtils.getStringIfConstant as (
  node: TSESTree.Node,
  initialScope?: TSESLint.Scope.Scope,
) => string | null` | ✓ |
| `hasSideEffect` | `(node: TSESTree.Node, sourceCode: SourceCode, options?: { considerGetters?: boolean; considerImplicitTypeConversion?: boolean; }) => boolean` | const | `eslintUtils.hasSideEffect as (
  node: TSESTree.Node,
  sourceCode: TSESLint.SourceCode,
  options?: {
    considerGetters?: boolean;
    considerImplicitTypeConversion?: boolean;
  },
) => boolean` | ✓ |
| `isParenthesized` | `{ (times: number, node: TSESTree.Node, sourceCode: SourceCode): boolean; (node: TSESTree.Node, sourceCode: SourceCode): boolean; }` | const | `eslintUtils.isParenthesized as {
  (
    times: number,
    node: TSESTree.Node,
    sourceCode: TSESLint.SourceCode,
  ): boolean;

  /**
   * Check whether a given node is parenthesized or not.
   * This function detects it correctly even if it's parenthesized by specific syntax.
   *
   * @see {@link https://eslint-community.github.io/eslint-utils/api/ast-utils.html#isparenthesized}
   * @returns `true` if the node is parenthesized.
   * If `times` was given, it returns `true` only if the node is parenthesized the `times` times.
   * For example, `isParenthesized(2, node, sourceCode)` returns true for `((foo))`, but not for `(foo)`.
   */
  (node: TSESTree.Node, sourceCode: TSESLint.SourceCode): boolean;
}` | ✓ |


---