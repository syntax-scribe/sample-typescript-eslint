[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-parameter-property-assignment.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-parameter-property-assignment.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getStaticStringValue` | `../util` |
| `nullThrows` | `../util` |


---

## Functions

### `isThisMemberExpression(node: TSESTree.Node): node is TSESTree.MemberExpression`

<details><summary>Code</summary>

```ts
function isThisMemberExpression(
      node: TSESTree.Node,
    ): node is TSESTree.MemberExpression {
      return (
        node.type === AST_NODE_TYPES.MemberExpression &&
        node.object.type === AST_NODE_TYPES.ThisExpression
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.MemberExpression`
### `getPropertyName(node: TSESTree.Node): string | null`

<details><summary>Code</summary>

```ts
function getPropertyName(node: TSESTree.Node): string | null {
      if (!isThisMemberExpression(node)) {
        return null;
      }

      if (node.property.type === AST_NODE_TYPES.Identifier) {
        return node.property.name;
      }
      if (node.computed) {
        return getStaticStringValue(node.property);
      }
      return null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `string | null`
- **Calls**:
  - `isThisMemberExpression`
  - `getStaticStringValue (from ../util)`
### `findParentFunction(node: TSESTree.Node | undefined): | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | undefined`

<details><summary>Code</summary>

```ts
function findParentFunction(
      node: TSESTree.Node | undefined,
    ):
      | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | undefined {
      if (
        !node ||
        node.type === AST_NODE_TYPES.FunctionDeclaration ||
        node.type === AST_NODE_TYPES.FunctionExpression ||
        node.type === AST_NODE_TYPES.ArrowFunctionExpression
      ) {
        return node;
      }
      return findParentFunction(node.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | undefined`
- **Return Type**: `| TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | undefined`
- **Calls**:
  - `findParentFunction`
### `findParentPropertyDefinition(node: TSESTree.Node | undefined): TSESTree.PropertyDefinition | undefined`

<details><summary>Code</summary>

```ts
function findParentPropertyDefinition(
      node: TSESTree.Node | undefined,
    ): TSESTree.PropertyDefinition | undefined {
      if (!node || node.type === AST_NODE_TYPES.PropertyDefinition) {
        return node;
      }
      return findParentPropertyDefinition(node.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | undefined`
- **Return Type**: `TSESTree.PropertyDefinition | undefined`
- **Calls**:
  - `findParentPropertyDefinition`
### `isConstructorFunctionExpression(node: TSESTree.Node | undefined): node is TSESTree.FunctionExpression`

<details><summary>Code</summary>

```ts
function isConstructorFunctionExpression(
      node: TSESTree.Node | undefined,
    ): node is TSESTree.FunctionExpression {
      return (
        node?.type === AST_NODE_TYPES.FunctionExpression &&
        ASTUtils.isConstructor(node.parent)
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | undefined`
- **Return Type**: `node is TSESTree.FunctionExpression`
- **Calls**:
  - `ASTUtils.isConstructor`
### `isReferenceFromParameter(node: TSESTree.Identifier): boolean`

<details><summary>Code</summary>

```ts
function isReferenceFromParameter(node: TSESTree.Identifier): boolean {
      const scope = context.sourceCode.getScope(node);

      const rightRef = scope.references.find(
        ref => ref.identifier.name === node.name,
      );
      return rightRef?.resolved?.defs.at(0)?.type === DefinitionType.Parameter;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getScope`
  - `scope.references.find`
  - `rightRef?.resolved?.defs.at`
### `isParameterPropertyWithName(node: TSESTree.Parameter, name: string): boolean`

<details><summary>Code</summary>

```ts
function isParameterPropertyWithName(
      node: TSESTree.Parameter,
      name: string,
    ): boolean {
      return (
        node.type === AST_NODE_TYPES.TSParameterProperty &&
        ((node.parameter.type === AST_NODE_TYPES.Identifier && // constructor (public foo) {}
          node.parameter.name === name) ||
          (node.parameter.type === AST_NODE_TYPES.AssignmentPattern && // constructor (public foo = 1) {}
            node.parameter.left.type === AST_NODE_TYPES.Identifier &&
            node.parameter.left.name === name))
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Parameter`
  - `name: string`
- **Return Type**: `boolean`
### `getIdentifier(node: TSESTree.Node): TSESTree.Identifier | null`

<details><summary>Code</summary>

```ts
function getIdentifier(node: TSESTree.Node): TSESTree.Identifier | null {
      if (node.type === AST_NODE_TYPES.Identifier) {
        return node;
      }
      if (
        node.type === AST_NODE_TYPES.TSAsExpression ||
        node.type === AST_NODE_TYPES.TSNonNullExpression
      ) {
        return getIdentifier(node.expression);
      }
      return null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Identifier | null`
- **Calls**:
  - `getIdentifier`
### `isArrowIIFE(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isArrowIIFE(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.ArrowFunctionExpression &&
        node.parent.type === AST_NODE_TYPES.CallExpression
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`

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