[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `explicitReturnTypeUtils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 16 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/explicitReturnTypeUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `isConstructor` | `./astUtils` |
| `isSetter` | `./astUtils` |
| `isTypeAssertion` | `./astUtils` |
| `getFunctionHeadLoc` | `./getFunctionHeadLoc` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `objectExpr` | `any` | const | `property.parent` | ✗ |
| `parent` | `any` | const | `objectExpr.parent` | ✗ |
| `body` | `any` | let/var | `node.body` | ✗ |
| `ancestor` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |
| `isReturnStatement` | `boolean` | const | `ancestor.type === AST_NODE_TYPES.ReturnStatement` | ✗ |
| `isBodylessArrow` | `boolean` | const | `ancestor.type === AST_NODE_TYPES.ArrowFunctionExpression &&
    ancestor.body.type !== AST_NODE_TYPES.BlockStatement` | ✗ |


---

## Functions

### `isVariableDeclaratorWithTypeAnnotation(node: TSESTree.Node): node is TSESTree.VariableDeclarator`

<details><summary>Code</summary>

```ts
function isVariableDeclaratorWithTypeAnnotation(
  node: TSESTree.Node,
): node is TSESTree.VariableDeclarator {
  return (
    node.type === AST_NODE_TYPES.VariableDeclarator && !!node.id.typeAnnotation
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is a variable declarator with a type annotation.
 * ```
 * const x: Foo = ...
 * ```
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.VariableDeclarator`
### `isPropertyDefinitionWithTypeAnnotation(node: TSESTree.Node): node is TSESTree.PropertyDefinition`

<details><summary>Code</summary>

```ts
function isPropertyDefinitionWithTypeAnnotation(
  node: TSESTree.Node,
): node is TSESTree.PropertyDefinition {
  return (
    node.type === AST_NODE_TYPES.PropertyDefinition && !!node.typeAnnotation
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is a class property with a type annotation.
 * ```
 * public x: Foo = ...
 * ```
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.PropertyDefinition`
### `isFunctionArgument(parent: TSESTree.Node, callee: FunctionExpression): parent is TSESTree.CallExpression`

<details><summary>Code</summary>

```ts
function isFunctionArgument(
  parent: TSESTree.Node,
  callee?: FunctionExpression,
): parent is TSESTree.CallExpression {
  return (
    parent.type === AST_NODE_TYPES.CallExpression &&
    // make sure this isn't an IIFE
    parent.callee !== callee
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node belongs to:
 * ```
 * foo(() => 1)
 * ```
 */
```

- **Parameters**:
  - `parent: TSESTree.Node`
  - `callee: FunctionExpression`
- **Return Type**: `parent is TSESTree.CallExpression`
- **Internal Comments**:
```
// make sure this isn't an IIFE (x3)
```

### `isTypedJSX(node: TSESTree.Node): node is TSESTree.JSXExpressionContainer | TSESTree.JSXSpreadAttribute`

<details><summary>Code</summary>

```ts
function isTypedJSX(
  node: TSESTree.Node,
): node is TSESTree.JSXExpressionContainer | TSESTree.JSXSpreadAttribute {
  return (
    node.type === AST_NODE_TYPES.JSXExpressionContainer ||
    node.type === AST_NODE_TYPES.JSXSpreadAttribute
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is type-constrained in JSX
 * ```
 * <Foo x={() => {}} />
 * <Bar>{() => {}}</Bar>
 * <Baz {...props} />
 * ```
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.JSXExpressionContainer | TSESTree.JSXSpreadAttribute`
### `isTypedParent(parent: TSESTree.Node, callee: FunctionExpression): boolean`

<details><summary>Code</summary>

```ts
function isTypedParent(
  parent: TSESTree.Node,
  callee?: FunctionExpression,
): boolean {
  return (
    isTypeAssertion(parent) ||
    isVariableDeclaratorWithTypeAnnotation(parent) ||
    isDefaultFunctionParameterWithTypeAnnotation(parent) ||
    isPropertyDefinitionWithTypeAnnotation(parent) ||
    isFunctionArgument(parent, callee) ||
    isTypedJSX(parent)
  );
}
```
</details>

- **Parameters**:
  - `parent: TSESTree.Node`
  - `callee: FunctionExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeAssertion (from ./astUtils)`
  - `isVariableDeclaratorWithTypeAnnotation`
  - `isDefaultFunctionParameterWithTypeAnnotation`
  - `isPropertyDefinitionWithTypeAnnotation`
  - `isFunctionArgument`
  - `isTypedJSX`
### `isDefaultFunctionParameterWithTypeAnnotation(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isDefaultFunctionParameterWithTypeAnnotation(
  node: TSESTree.Node,
): boolean {
  return (
    node.type === AST_NODE_TYPES.AssignmentPattern &&
    node.left.typeAnnotation != null
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isConstructorArgument(node: TSESTree.Node): node is TSESTree.NewExpression`

<details><summary>Code</summary>

```ts
function isConstructorArgument(
  node: TSESTree.Node,
): node is TSESTree.NewExpression {
  return node.type === AST_NODE_TYPES.NewExpression;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node belongs to:
 * ```
 * new Foo(() => {})
 *         ^^^^^^^^
 * ```
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.NewExpression`
### `isPropertyOfObjectWithType(property: TSESTree.Node | undefined): boolean`

<details><summary>Code</summary>

```ts
function isPropertyOfObjectWithType(
  property: TSESTree.Node | undefined,
): boolean {
  if (!property || property.type !== AST_NODE_TYPES.Property) {
    return false;
  }
  const objectExpr = property.parent;
  if (objectExpr.type !== AST_NODE_TYPES.ObjectExpression) {
    return false;
  }

  const parent = objectExpr.parent;

  return isTypedParent(parent) || isPropertyOfObjectWithType(parent);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a node is a property or a nested property of a typed object:
 * ```
 * const x: Foo = { prop: () => {} }
 * const x = { prop: () => {} } as Foo
 * const x = <Foo>{ prop: () => {} }
 * const x: Foo = { bar: { prop: () => {} } }
 * ```
 */
```

- **Parameters**:
  - `property: TSESTree.Node | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypedParent`
  - `isPropertyOfObjectWithType`
### `doesImmediatelyReturnFunctionExpression({
  node,
  returns,
}: FunctionInfo<FunctionNode>): boolean`

<details><summary>Code</summary>

```ts
export function doesImmediatelyReturnFunctionExpression({
  node,
  returns,
}: FunctionInfo<FunctionNode>): boolean {
  if (
    node.type === AST_NODE_TYPES.ArrowFunctionExpression &&
    ASTUtils.isFunction(node.body)
  ) {
    return true;
  }

  if (returns.length === 0) {
    return false;
  }

  return returns.every(
    node => node.argument && ASTUtils.isFunction(node.argument),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a function belongs to:
 * ```
 * () => () => ...
 * () => function () { ... }
 * () => { return () => ... }
 * () => { return function () { ... } }
 * function fn() { return () => ... }
 * function fn() { return function() { ... } }
 * ```
 */
```

- **Parameters**:
  - `{
  node,
  returns,
}: FunctionInfo<FunctionNode>`
- **Return Type**: `boolean`
- **Calls**:
  - `ASTUtils.isFunction`
  - `returns.every`
### `isConstAssertion(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isConstAssertion(node: TSESTree.Node): boolean {
  if (isTypeAssertion(node)) {
    const { typeAnnotation } = node;
    if (typeAnnotation.type === AST_NODE_TYPES.TSTypeReference) {
      const { typeName } = typeAnnotation;
      if (
        typeName.type === AST_NODE_TYPES.Identifier &&
        typeName.name === 'const'
      ) {
        return true;
      }
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a function belongs to:
 * ```
 * ({ action: 'xxx' } as const)
 * ```
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeAssertion (from ./astUtils)`
### `isTypedFunctionExpression(node: FunctionExpression, options: Options): boolean`

<details><summary>Code</summary>

```ts
export function isTypedFunctionExpression(
  node: FunctionExpression,
  options: Options,
): boolean {
  const parent = ESLintUtils.nullThrows(
    node.parent,
    ESLintUtils.NullThrowsReasons.MissingParent,
  );

  if (!options.allowTypedFunctionExpressions) {
    return false;
  }

  return (
    isTypedParent(parent, node) ||
    isPropertyOfObjectWithType(parent) ||
    isConstructorArgument(parent)
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * True when the provided function expression is typed.
 */
```

- **Parameters**:
  - `node: FunctionExpression`
  - `options: Options`
- **Return Type**: `boolean`
- **Calls**:
  - `ESLintUtils.nullThrows`
  - `isTypedParent`
  - `isPropertyOfObjectWithType`
  - `isConstructorArgument`
### `isValidFunctionExpressionReturnType(node: FunctionExpression, options: Options): boolean`

<details><summary>Code</summary>

```ts
export function isValidFunctionExpressionReturnType(
  node: FunctionExpression,
  options: Options,
): boolean {
  if (isTypedFunctionExpression(node, options)) {
    return true;
  }

  const parent = ESLintUtils.nullThrows(
    node.parent,
    ESLintUtils.NullThrowsReasons.MissingParent,
  );
  if (
    options.allowExpressions &&
    parent.type !== AST_NODE_TYPES.VariableDeclarator &&
    parent.type !== AST_NODE_TYPES.MethodDefinition &&
    parent.type !== AST_NODE_TYPES.ExportDefaultDeclaration &&
    parent.type !== AST_NODE_TYPES.PropertyDefinition
  ) {
    return true;
  }

  // https://github.com/typescript-eslint/typescript-eslint/issues/653
  if (
    !options.allowDirectConstAssertionInArrowFunctions ||
    node.type !== AST_NODE_TYPES.ArrowFunctionExpression
  ) {
    return false;
  }

  let body = node.body;
  while (body.type === AST_NODE_TYPES.TSSatisfiesExpression) {
    body = body.expression;
  }

  return isConstAssertion(body);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check whether the function expression return type is either typed or valid
 * with the provided options.
 */
```

- **Parameters**:
  - `node: FunctionExpression`
  - `options: Options`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypedFunctionExpression`
  - `ESLintUtils.nullThrows`
  - `isConstAssertion`
- **Internal Comments**:
```
// https://github.com/typescript-eslint/typescript-eslint/issues/653
```

### `isValidFunctionReturnType({ node, returns }: FunctionInfo<FunctionNode>, options: Options): boolean`

<details><summary>Code</summary>

```ts
function isValidFunctionReturnType(
  { node, returns }: FunctionInfo<FunctionNode>,
  options: Options,
): boolean {
  if (
    options.allowHigherOrderFunctions &&
    doesImmediatelyReturnFunctionExpression({ node, returns })
  ) {
    return true;
  }

  return (
    node.returnType != null ||
    isConstructor(node.parent) ||
    isSetter(node.parent)
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check that the function expression or declaration is valid.
 */
```

- **Parameters**:
  - `{ node, returns }: FunctionInfo<FunctionNode>`
  - `options: Options`
- **Return Type**: `boolean`
- **Calls**:
  - `doesImmediatelyReturnFunctionExpression`
  - `isConstructor (from ./astUtils)`
  - `isSetter (from ./astUtils)`
### `checkFunctionReturnType({ node, returns }: FunctionInfo<FunctionNode>, options: Options, sourceCode: TSESLint.SourceCode, report: (loc: TSESTree.SourceLocation) => void): void`

<details><summary>Code</summary>

```ts
export function checkFunctionReturnType(
  { node, returns }: FunctionInfo<FunctionNode>,
  options: Options,
  sourceCode: TSESLint.SourceCode,
  report: (loc: TSESTree.SourceLocation) => void,
): void {
  if (isValidFunctionReturnType({ node, returns }, options)) {
    return;
  }

  report(getFunctionHeadLoc(node, sourceCode));
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a function declaration/expression has a return type.
 */
```

- **Parameters**:
  - `{ node, returns }: FunctionInfo<FunctionNode>`
  - `options: Options`
  - `sourceCode: TSESLint.SourceCode`
  - `report: (loc: TSESTree.SourceLocation) => void`
- **Return Type**: `void`
- **Calls**:
  - `isValidFunctionReturnType`
  - `report`
  - `getFunctionHeadLoc (from ./getFunctionHeadLoc)`
### `checkFunctionExpressionReturnType(info: FunctionInfo<FunctionExpression>, options: Options, sourceCode: TSESLint.SourceCode, report: (loc: TSESTree.SourceLocation) => void): void`

<details><summary>Code</summary>

```ts
export function checkFunctionExpressionReturnType(
  info: FunctionInfo<FunctionExpression>,
  options: Options,
  sourceCode: TSESLint.SourceCode,
  report: (loc: TSESTree.SourceLocation) => void,
): void {
  if (isValidFunctionExpressionReturnType(info.node, options)) {
    return;
  }

  checkFunctionReturnType(info, options, sourceCode, report);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if a function declaration/expression has a return type.
 */
```

- **Parameters**:
  - `info: FunctionInfo<FunctionExpression>`
  - `options: Options`
  - `sourceCode: TSESLint.SourceCode`
  - `report: (loc: TSESTree.SourceLocation) => void`
- **Return Type**: `void`
- **Calls**:
  - `isValidFunctionExpressionReturnType`
  - `checkFunctionReturnType`
### `ancestorHasReturnType(node: FunctionNode): boolean`

<details><summary>Code</summary>

```ts
export function ancestorHasReturnType(node: FunctionNode): boolean {
  let ancestor: TSESTree.Node | undefined = node.parent;

  if (ancestor.type === AST_NODE_TYPES.Property) {
    ancestor = ancestor.value;
  }

  // if the ancestor is not a return, then this function was not returned at all, so we can exit early
  const isReturnStatement = ancestor.type === AST_NODE_TYPES.ReturnStatement;
  const isBodylessArrow =
    ancestor.type === AST_NODE_TYPES.ArrowFunctionExpression &&
    ancestor.body.type !== AST_NODE_TYPES.BlockStatement;
  if (!isReturnStatement && !isBodylessArrow) {
    return false;
  }

  while (ancestor) {
    switch (ancestor.type) {
      case AST_NODE_TYPES.ArrowFunctionExpression:
      case AST_NODE_TYPES.FunctionExpression:
      case AST_NODE_TYPES.FunctionDeclaration:
        if (ancestor.returnType) {
          return true;
        }
        break;

      // const x: Foo = () => {};
      // Assume that a typed variable types the function expression
      case AST_NODE_TYPES.VariableDeclarator:
        return !!ancestor.id.typeAnnotation;

      case AST_NODE_TYPES.PropertyDefinition:
        return !!ancestor.typeAnnotation;
      case AST_NODE_TYPES.ExpressionStatement:
        return false;
    }

    ancestor = ancestor.parent;
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check whether any ancestor of the provided function has a valid return type.
 */
```

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// if the ancestor is not a return, then this function was not returned at all, so we can exit early (x2)
// const x: Foo = () => {};
// Assume that a typed variable types the function expression
```


---

## Interfaces

### `FunctionInfo<T extends FunctionNode>`

<details><summary>Interface Code</summary>

```ts
export interface FunctionInfo<T extends FunctionNode> {
  node: T;
  returns: TSESTree.ReturnStatement[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `node` | `T` | ✗ |  |
| `returns` | `TSESTree.ReturnStatement[]` | ✗ |  |

### `Options`

<details><summary>Interface Code</summary>

```ts
interface Options {
  allowDirectConstAssertionInArrowFunctions?: boolean;
  allowExpressions?: boolean;
  allowHigherOrderFunctions?: boolean;
  allowTypedFunctionExpressions?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowDirectConstAssertionInArrowFunctions` | `boolean` | ✓ |  |
| `allowExpressions` | `boolean` | ✓ |  |
| `allowHigherOrderFunctions` | `boolean` | ✓ |  |
| `allowTypedFunctionExpressions` | `boolean` | ✓ |  |


---

## Type Aliases

### `FunctionExpression`

```ts
type FunctionExpression = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionExpression;
```

### `FunctionNode`

```ts
type FunctionNode = FunctionExpression | TSESTree.FunctionDeclaration;
```


---