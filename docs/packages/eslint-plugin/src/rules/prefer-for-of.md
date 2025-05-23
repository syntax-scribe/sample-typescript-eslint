[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-for-of.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 8
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-for-of.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isAssignee` | `../util` |


---

## Functions

### `isSingleVariableDeclaration(node: TSESTree.Node | null): node is TSESTree.VariableDeclaration`

<details><summary>Code</summary>

```ts
function isSingleVariableDeclaration(
      node: TSESTree.Node | null,
    ): node is TSESTree.VariableDeclaration {
      return (
        node?.type === AST_NODE_TYPES.VariableDeclaration &&
        node.kind !== 'const' &&
        node.declarations.length === 1
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null`
- **Return Type**: `node is TSESTree.VariableDeclaration`
### `isLiteral(node: TSESTree.Expression | TSESTree.PrivateIdentifier, value: number): boolean`

<details><summary>Code</summary>

```ts
function isLiteral(
      node: TSESTree.Expression | TSESTree.PrivateIdentifier,
      value: number,
    ): boolean {
      return node.type === AST_NODE_TYPES.Literal && node.value === value;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression | TSESTree.PrivateIdentifier`
  - `value: number`
- **Return Type**: `boolean`
### `isZeroInitialized(node: TSESTree.VariableDeclarator): boolean`

<details><summary>Code</summary>

```ts
function isZeroInitialized(node: TSESTree.VariableDeclarator): boolean {
      return node.init != null && isLiteral(node.init, 0);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.VariableDeclarator`
- **Return Type**: `boolean`
- **Calls**:
  - `isLiteral`
### `isMatchingIdentifier(node: TSESTree.Expression | TSESTree.PrivateIdentifier, name: string): boolean`

<details><summary>Code</summary>

```ts
function isMatchingIdentifier(
      node: TSESTree.Expression | TSESTree.PrivateIdentifier,
      name: string,
    ): boolean {
      return node.type === AST_NODE_TYPES.Identifier && node.name === name;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression | TSESTree.PrivateIdentifier`
  - `name: string`
- **Return Type**: `boolean`
### `isLessThanLengthExpression(node: TSESTree.Node | null, name: string): TSESTree.Expression | null`

<details><summary>Code</summary>

```ts
function isLessThanLengthExpression(
      node: TSESTree.Node | null,
      name: string,
    ): TSESTree.Expression | null {
      if (
        node?.type === AST_NODE_TYPES.BinaryExpression &&
        node.operator === '<' &&
        isMatchingIdentifier(node.left, name) &&
        node.right.type === AST_NODE_TYPES.MemberExpression &&
        isMatchingIdentifier(node.right.property, 'length')
      ) {
        return node.right.object;
      }
      return null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null`
  - `name: string`
- **Return Type**: `TSESTree.Expression | null`
- **Calls**:
  - `isMatchingIdentifier`
### `isIncrement(node: TSESTree.Node | null, name: string): boolean`

<details><summary>Code</summary>

```ts
function isIncrement(node: TSESTree.Node | null, name: string): boolean {
      if (!node) {
        return false;
      }

      switch (node.type) {
        case AST_NODE_TYPES.UpdateExpression:
          // x++ or ++x
          return (
            node.operator === '++' && isMatchingIdentifier(node.argument, name)
          );
        case AST_NODE_TYPES.AssignmentExpression:
          if (isMatchingIdentifier(node.left, name)) {
            if (node.operator === '+=') {
              // x += 1
              return isLiteral(node.right, 1);
            }
            if (node.operator === '=') {
              // x = x + 1 or x = 1 + x
              const expr = node.right;
              return (
                expr.type === AST_NODE_TYPES.BinaryExpression &&
                expr.operator === '+' &&
                ((isMatchingIdentifier(expr.left, name) &&
                  isLiteral(expr.right, 1)) ||
                  (isLiteral(expr.left, 1) &&
                    isMatchingIdentifier(expr.right, name)))
              );
            }
          }
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null`
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `isMatchingIdentifier`
  - `isLiteral`
- **Internal Comments**:
```
// x++ or ++x
// x += 1
// x = x + 1 or x = 1 + x (x2)
```

### `contains(outer: TSESTree.Node, inner: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function contains(outer: TSESTree.Node, inner: TSESTree.Node): boolean {
      return (
        outer.range[0] <= inner.range[0] && outer.range[1] >= inner.range[1]
      );
    }
```
</details>

- **Parameters**:
  - `outer: TSESTree.Node`
  - `inner: TSESTree.Node`
- **Return Type**: `boolean`
### `isIndexOnlyUsedWithArray(body: TSESTree.Statement, indexVar: TSESLint.Scope.Variable, arrayExpression: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isIndexOnlyUsedWithArray(
      body: TSESTree.Statement,
      indexVar: TSESLint.Scope.Variable,
      arrayExpression: TSESTree.Expression,
    ): boolean {
      const arrayText = context.sourceCode.getText(arrayExpression);
      return indexVar.references.every(reference => {
        const id = reference.identifier;
        const node = id.parent;
        return (
          !contains(body, id) ||
          (node.type === AST_NODE_TYPES.MemberExpression &&
            node.object.type !== AST_NODE_TYPES.ThisExpression &&
            node.property === id &&
            context.sourceCode.getText(node.object) === arrayText &&
            !isAssignee(node))
        );
      });
    }
```
</details>

- **Parameters**:
  - `body: TSESTree.Statement`
  - `indexVar: TSESLint.Scope.Variable`
  - `arrayExpression: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getText`
  - `indexVar.references.every`
  - `contains`
  - `isAssignee (from ../util)`

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