[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-explicit-any.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 106 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-explicit-any.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `fixOrSuggest` | `{
          fix: TSESLint.ReportFixFunction | null;
          suggest: TSESLint.ReportSuggestionArray<MessageIds> | null;
        }` | const | `{
          fix: null,
          suggest: isKeyofAny
            ? [
                {
                  messageId: 'suggestPropertyKey',
                  fix: createPropertyKeyFixer(node),
                },
              ]
            : [
                {
                  messageId: 'suggestUnknown',
                  fix: fixer => fixer.replaceText(node, 'unknown'),
                },
                {
                  messageId: 'suggestNever',
                  fix: fixer => fixer.replaceText(node, 'never'),
                },
              ],
        }` | ✗ |


---

## Functions

### `isNodeValidFunction(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeValidFunction(node: TSESTree.Node): boolean {
      return [
        AST_NODE_TYPES.ArrowFunctionExpression, // const x = (...args: any[]) => {};
        AST_NODE_TYPES.FunctionDeclaration, // function f(...args: any[]) {}
        AST_NODE_TYPES.FunctionExpression, // const x = function(...args: any[]) {};
        AST_NODE_TYPES.TSCallSignatureDeclaration, // type T = {(...args: any[]): unknown};
        AST_NODE_TYPES.TSConstructorType, // type T = new (...args: any[]) => unknown
        AST_NODE_TYPES.TSConstructSignatureDeclaration, // type T = {new (...args: any[]): unknown};
        AST_NODE_TYPES.TSDeclareFunction, // declare function _8(...args: any[]): unknown;
        AST_NODE_TYPES.TSEmptyBodyFunctionExpression, // declare class A { f(...args: any[]): unknown; }
        AST_NODE_TYPES.TSFunctionType, // type T = (...args: any[]) => unknown;
        AST_NODE_TYPES.TSMethodSignature, // type T = {f(...args: any[]): unknown};
      ].includes(node.type);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is an arrow function, function/constructor declaration or function expression
     * @param node the node to be validated.
     * @returns true if the node is any kind of function declaration or expression
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `[
        AST_NODE_TYPES.ArrowFunctionExpression, // const x = (...args: any[]) => {};
        AST_NODE_TYPES.FunctionDeclaration, // function f(...args: any[]) {}
        AST_NODE_TYPES.FunctionExpression, // const x = function(...args: any[]) {};
        AST_NODE_TYPES.TSCallSignatureDeclaration, // type T = {(...args: any[]): unknown};
        AST_NODE_TYPES.TSConstructorType, // type T = new (...args: any[]) => unknown
        AST_NODE_TYPES.TSConstructSignatureDeclaration, // type T = {new (...args: any[]): unknown};
        AST_NODE_TYPES.TSDeclareFunction, // declare function _8(...args: any[]): unknown;
        AST_NODE_TYPES.TSEmptyBodyFunctionExpression, // declare class A { f(...args: any[]): unknown; }
        AST_NODE_TYPES.TSFunctionType, // type T = (...args: any[]) => unknown;
        AST_NODE_TYPES.TSMethodSignature, // type T = {f(...args: any[]): unknown};
      ].includes`
### `isNodeRestElementInFunction(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeRestElementInFunction(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.RestElement &&
        isNodeValidFunction(node.parent)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is a rest element child node of a function
     * @param node the node to be validated.
     * @returns true if the node is a rest element child node of a function
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeValidFunction`
### `isNodeReadonlyTSTypeOperator(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeReadonlyTSTypeOperator(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.TSTypeOperator &&
        node.operator === 'readonly'
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is a TSTypeOperator node with a readonly operator
     * @param node the node to be validated.
     * @returns true if the node is a TSTypeOperator node with a readonly operator
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isNodeValidArrayTSTypeReference(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeValidArrayTSTypeReference(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.TSTypeReference &&
        node.typeName.type === AST_NODE_TYPES.Identifier &&
        ['Array', 'ReadonlyArray'].includes(node.typeName.name)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is a TSTypeReference node with an Array identifier
     * @param node the node to be validated.
     * @returns true if the node is a TSTypeReference node with an Array identifier
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `['Array', 'ReadonlyArray'].includes`
### `isNodeValidTSType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeValidTSType(node: TSESTree.Node): boolean {
      return (
        isNodeReadonlyTSTypeOperator(node) ||
        isNodeValidArrayTSTypeReference(node)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is a valid TSTypeOperator or TSTypeReference node
     * @param node the node to be validated.
     * @returns true if the node is a valid TSTypeOperator or TSTypeReference node
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeReadonlyTSTypeOperator`
  - `isNodeValidArrayTSTypeReference`
### `isGreatGrandparentRestElement(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isGreatGrandparentRestElement(node: TSESTree.Node): boolean {
      return (
        node.parent?.parent?.parent != null &&
        isNodeRestElementInFunction(node.parent.parent.parent)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the great grand-parent node is a RestElement node in a function
     * @param node the node to be validated.
     * @returns true if the great grand-parent node is a RestElement node in a function
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeRestElementInFunction`
### `isGreatGreatGrandparentRestElement(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isGreatGreatGrandparentRestElement(node: TSESTree.Node): boolean {
      return (
        node.parent?.parent?.parent?.parent != null &&
        isNodeValidTSType(node.parent.parent) &&
        isNodeRestElementInFunction(node.parent.parent.parent.parent)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the great great grand-parent node is a valid RestElement node in a function
     * @param node the node to be validated.
     * @returns true if the great great grand-parent node is a valid RestElement node in a function
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isNodeValidTSType`
  - `isNodeRestElementInFunction`
### `isNodeDescendantOfRestElementInFunction(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNodeDescendantOfRestElementInFunction(
      node: TSESTree.Node,
    ): boolean {
      return (
        isGreatGrandparentRestElement(node) ||
        isGreatGreatGrandparentRestElement(node)
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the great grand-parent or the great great grand-parent node is a RestElement node
     * @param node the node to be validated.
     * @returns true if the great grand-parent or the great great grand-parent node is a RestElement node
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isGreatGrandparentRestElement`
  - `isGreatGreatGrandparentRestElement`
### `isNodeWithinKeyofAny(node: TSESTree.TSAnyKeyword): boolean`

<details><summary>Code</summary>

```ts
function isNodeWithinKeyofAny(node: TSESTree.TSAnyKeyword): boolean {
      return (
        node.parent.type === AST_NODE_TYPES.TSTypeOperator &&
        node.parent.operator === 'keyof'
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the node is within a keyof any expression
     * @param node the node to be validated.
     * @returns true if the node is within a keyof any expression, false otherwise
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.TSAnyKeyword`
- **Return Type**: `boolean`
### `createPropertyKeyFixer(node: TSESTree.TSAnyKeyword): (fixer: TSESLint.RuleFixer) => any`

<details><summary>Code</summary>

```ts
function createPropertyKeyFixer(node: TSESTree.TSAnyKeyword) {
      return (fixer: TSESLint.RuleFixer) => {
        return fixer.replaceText(node.parent, 'PropertyKey');
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Creates a fixer that replaces a keyof any with PropertyKey
     * @param node the node to be fixed.
     * @returns a function that will fix the node.
     * @private
     */
```

- **Parameters**:
  - `node: TSESTree.TSAnyKeyword`
- **Return Type**: `(fixer: TSESLint.RuleFixer) => any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'unknown')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'never')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    fixToUnknown?: boolean;
    ignoreRestArgs?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'suggestNever'
  | 'suggestPropertyKey'
  | 'suggestUnknown'
  | 'unexpectedAny';
```


---