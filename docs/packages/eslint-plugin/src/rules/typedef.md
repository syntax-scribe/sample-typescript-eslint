[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typedef.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/typedef.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `current` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |
| `annotationNode` | `TSESTree.Node | undefined` | let/var | `*not shown*` | ✗ |
| `ancestor` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |
| `current` | `TSESTree.Node | undefined` | let/var | `node.parent` | ✗ |


---

## Functions

### `report(location: TSESTree.Node, name: string): void`

<details><summary>Code</summary>

```ts
function report(location: TSESTree.Node, name?: string): void {
      context.report({
        node: location,
        messageId: name ? 'expectedTypedefNamed' : 'expectedTypedef',
        data: { name },
      });
    }
```
</details>

- **Parameters**:
  - `location: TSESTree.Node`
  - `name: string`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `getNodeName(node: TSESTree.Parameter | TSESTree.PropertyName): string | undefined`

<details><summary>Code</summary>

```ts
function getNodeName(
      node: TSESTree.Parameter | TSESTree.PropertyName,
    ): string | undefined {
      return node.type === AST_NODE_TYPES.Identifier ? node.name : undefined;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Parameter | TSESTree.PropertyName`
- **Return Type**: `string | undefined`
### `isForOfStatementContext(node: TSESTree.ArrayPattern | TSESTree.ObjectPattern): boolean`

<details><summary>Code</summary>

```ts
function isForOfStatementContext(
      node: TSESTree.ArrayPattern | TSESTree.ObjectPattern,
    ): boolean {
      let current: TSESTree.Node | undefined = node.parent;
      while (current) {
        switch (current.type) {
          case AST_NODE_TYPES.VariableDeclarator:
          case AST_NODE_TYPES.VariableDeclaration:
          case AST_NODE_TYPES.ObjectPattern:
          case AST_NODE_TYPES.ArrayPattern:
          case AST_NODE_TYPES.Property:
            current = current.parent;
            break;

          case AST_NODE_TYPES.ForOfStatement:
            return true;

          default:
            current = undefined;
        }
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrayPattern | TSESTree.ObjectPattern`
- **Return Type**: `boolean`
### `checkParameters(params: TSESTree.Parameter[]): void`

<details><summary>Code</summary>

```ts
function checkParameters(params: TSESTree.Parameter[]): void {
      for (const param of params) {
        let annotationNode: TSESTree.Node | undefined;

        switch (param.type) {
          case AST_NODE_TYPES.AssignmentPattern:
            annotationNode = param.left;
            break;
          case AST_NODE_TYPES.TSParameterProperty:
            annotationNode = param.parameter;

            // Check TS parameter property with default value like `constructor(private param: string = 'something') {}`
            if (annotationNode.type === AST_NODE_TYPES.AssignmentPattern) {
              annotationNode = annotationNode.left;
            }

            break;
          default:
            annotationNode = param;
            break;
        }

        if (!annotationNode.typeAnnotation) {
          report(param, getNodeName(param));
        }
      }
    }
```
</details>

- **Parameters**:
  - `params: TSESTree.Parameter[]`
- **Return Type**: `void`
- **Calls**:
  - `report`
  - `getNodeName`
- **Internal Comments**:
```
// Check TS parameter property with default value like `constructor(private param: string = 'something') {}`
```

### `isVariableDeclarationIgnoreFunction(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isVariableDeclarationIgnoreFunction(node: TSESTree.Node): boolean {
      return (
        variableDeclarationIgnoreFunction === true &&
        (node.type === AST_NODE_TYPES.ArrowFunctionExpression ||
          node.type === AST_NODE_TYPES.FunctionExpression)
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isAncestorHasTypeAnnotation(node: TSESTree.ArrayPattern | TSESTree.ObjectPattern): boolean`

<details><summary>Code</summary>

```ts
function isAncestorHasTypeAnnotation(
      node: TSESTree.ArrayPattern | TSESTree.ObjectPattern,
    ): boolean {
      let ancestor: TSESTree.Node | undefined = node.parent;

      while (ancestor) {
        if (
          (ancestor.type === AST_NODE_TYPES.ObjectPattern ||
            ancestor.type === AST_NODE_TYPES.ArrayPattern) &&
          ancestor.typeAnnotation
        ) {
          return true;
        }

        ancestor = ancestor.parent;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrayPattern | TSESTree.ObjectPattern`
- **Return Type**: `boolean`

---

## Type Aliases

### `Options`

```ts
type Options = [Partial<Record<OptionKeys, boolean>>];
```

### `MessageIds`

```ts
type MessageIds = 'expectedTypedef' | 'expectedTypedefNamed';
```


---

## Enums

### `const enum OptionKeys`

<details><summary>Enum Code</summary>

```ts
export const enum OptionKeys {
  ArrayDestructuring = 'arrayDestructuring',
  ArrowParameter = 'arrowParameter',
  MemberVariableDeclaration = 'memberVariableDeclaration',
  ObjectDestructuring = 'objectDestructuring',
  Parameter = 'parameter',
  PropertyDeclaration = 'propertyDeclaration',
  VariableDeclaration = 'variableDeclaration',
  VariableDeclarationIgnoreFunction = 'variableDeclarationIgnoreFunction',
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `ArrayDestructuring` | `arrayDestructuring` |  |
| `ArrowParameter` | `arrowParameter` |  |
| `MemberVariableDeclaration` | `memberVariableDeclaration` |  |
| `ObjectDestructuring` | `objectDestructuring` |  |
| `Parameter` | `parameter` |  |
| `PropertyDeclaration` | `propertyDeclaration` |  |
| `VariableDeclaration` | `variableDeclaration` |  |
| `VariableDeclarationIgnoreFunction` | `variableDeclarationIgnoreFunction` |  |


---