[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-literal-enum-member.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
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
📂 **`packages/eslint-plugin/src/rules/prefer-literal-enum-member.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getStaticStringValue` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `declaration` | `any` | const | `node.parent.parent` | ✗ |


---

## Functions

### `isIdentifierWithName(node: TSESTree.Node, name: string): boolean`

<details><summary>Code</summary>

```ts
function isIdentifierWithName(node: TSESTree.Node, name: string): boolean {
      return node.type === AST_NODE_TYPES.Identifier && node.name === name;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `name: string`
- **Return Type**: `boolean`
### `hasEnumMember(decl: TSESTree.TSEnumDeclaration, name: string): boolean`

<details><summary>Code</summary>

```ts
function hasEnumMember(
      decl: TSESTree.TSEnumDeclaration,
      name: string,
    ): boolean {
      return decl.body.members.some(
        member =>
          isIdentifierWithName(member.id, name) ||
          (member.id.type === AST_NODE_TYPES.Literal &&
            getStaticStringValue(member.id) === name),
      );
    }
```
</details>

- **Parameters**:
  - `decl: TSESTree.TSEnumDeclaration`
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `decl.body.members.some`
  - `isIdentifierWithName`
  - `getStaticStringValue (from ../util)`
### `isSelfEnumMember(decl: TSESTree.TSEnumDeclaration, node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isSelfEnumMember(
      decl: TSESTree.TSEnumDeclaration,
      node: TSESTree.Node,
    ): boolean {
      if (node.type === AST_NODE_TYPES.Identifier) {
        return hasEnumMember(decl, node.name);
      }

      if (
        node.type === AST_NODE_TYPES.MemberExpression &&
        isIdentifierWithName(node.object, decl.id.name)
      ) {
        if (node.property.type === AST_NODE_TYPES.Identifier) {
          return hasEnumMember(decl, node.property.name);
        }

        if (node.computed) {
          const propertyName = getStaticStringValue(node.property);
          if (propertyName) {
            return hasEnumMember(decl, propertyName);
          }
        }
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `decl: TSESTree.TSEnumDeclaration`
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `hasEnumMember`
  - `isIdentifierWithName`
  - `getStaticStringValue (from ../util)`
### `isAllowedInitializerExpressionRecursive(node: TSESTree.Expression | TSESTree.PrivateIdentifier, partOfBitwiseComputation: boolean): boolean`

<details><summary>Code</summary>

```ts
function isAllowedInitializerExpressionRecursive(
          node: TSESTree.Expression | TSESTree.PrivateIdentifier,
          partOfBitwiseComputation: boolean,
        ): boolean {
          // You can only refer to an enum member if it's part of a bitwise computation.
          // so C = B isn't allowed (special case), but C = A | B is.
          if (partOfBitwiseComputation && isSelfEnumMember(declaration, node)) {
            return true;
          }

          switch (node.type) {
            // any old literal
            case AST_NODE_TYPES.Literal:
              return true;

            // TemplateLiteral without expressions
            case AST_NODE_TYPES.TemplateLiteral:
              return node.expressions.length === 0;

            case AST_NODE_TYPES.UnaryExpression:
              // +123, -123, etc.
              if (['-', '+'].includes(node.operator)) {
                return isAllowedInitializerExpressionRecursive(
                  node.argument,
                  partOfBitwiseComputation,
                );
              }

              if (allowBitwiseExpressions) {
                return (
                  node.operator === '~' &&
                  isAllowedInitializerExpressionRecursive(node.argument, true)
                );
              }
              return false;

            case AST_NODE_TYPES.BinaryExpression:
              if (allowBitwiseExpressions) {
                return (
                  ['&', '^', '<<', '>>', '>>>', '|'].includes(node.operator) &&
                  isAllowedInitializerExpressionRecursive(node.left, true) &&
                  isAllowedInitializerExpressionRecursive(node.right, true)
                );
              }
              return false;

            default:
              return false;
          }
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression | TSESTree.PrivateIdentifier`
  - `partOfBitwiseComputation: boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `isSelfEnumMember`
  - `['-', '+'].includes`
  - `isAllowedInitializerExpressionRecursive`
  - `['&', '^', '<<', '>>', '>>>', '|'].includes`
- **Internal Comments**:
```
// You can only refer to an enum member if it's part of a bitwise computation.
// so C = B isn't allowed (special case), but C = A | B is.
// any old literal
// TemplateLiteral without expressions
// +123, -123, etc.
```


---