[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-return-this-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-return-this-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `forEachReturnStatement` | `../util` |
| `getParserServices` | `../util` |


---

## Functions

### `tryGetNameInType(name: string, typeNode: TSESTree.TypeNode): TSESTree.TSTypeReference | undefined`

<details><summary>Code</summary>

```ts
function tryGetNameInType(
      name: string,
      typeNode: TSESTree.TypeNode,
    ): TSESTree.TSTypeReference | undefined {
      if (
        typeNode.type === AST_NODE_TYPES.TSTypeReference &&
        typeNode.typeName.type === AST_NODE_TYPES.Identifier &&
        typeNode.typeName.name === name
      ) {
        return typeNode;
      }

      if (typeNode.type === AST_NODE_TYPES.TSUnionType) {
        for (const type of typeNode.types) {
          const found = tryGetNameInType(name, type);
          if (found) {
            return found;
          }
        }
      }

      return undefined;
    }
```
</details>

- **Parameters**:
  - `name: string`
  - `typeNode: TSESTree.TypeNode`
- **Return Type**: `TSESTree.TSTypeReference | undefined`
- **Calls**:
  - `tryGetNameInType`
### `isThisSpecifiedInParameters(originalFunc: FunctionLike): boolean`

<details><summary>Code</summary>

```ts
function isThisSpecifiedInParameters(originalFunc: FunctionLike): boolean {
      const firstArg = originalFunc.params.at(0);
      return (
        firstArg?.type === AST_NODE_TYPES.Identifier && firstArg.name === 'this'
      );
    }
```
</details>

- **Parameters**:
  - `originalFunc: FunctionLike`
- **Return Type**: `boolean`
- **Calls**:
  - `originalFunc.params.at`
### `isFunctionReturningThis(originalFunc: FunctionLike, originalClass: ClassLikeDeclaration): boolean`

<details><summary>Code</summary>

```ts
function isFunctionReturningThis(
      originalFunc: FunctionLike,
      originalClass: ClassLikeDeclaration,
    ): boolean {
      if (isThisSpecifiedInParameters(originalFunc)) {
        return false;
      }

      const func = services.esTreeNodeToTSNodeMap.get(originalFunc);

      if (!func.body) {
        return false;
      }

      const classType = services.getTypeAtLocation(
        originalClass,
      ) as ts.InterfaceType;

      if (func.body.kind !== ts.SyntaxKind.Block) {
        const type = checker.getTypeAtLocation(func.body);
        return classType.thisType === type;
      }

      let hasReturnThis = false;
      let hasReturnClassType = false as boolean;

      forEachReturnStatement(func.body as ts.Block, stmt => {
        const expr = stmt.expression;
        if (!expr) {
          return;
        }

        // fast check
        if (expr.kind === ts.SyntaxKind.ThisKeyword) {
          hasReturnThis = true;
          return;
        }

        const type = checker.getTypeAtLocation(expr);
        if (classType === type) {
          hasReturnClassType = true;
          return true;
        }

        if (classType.thisType === type) {
          hasReturnThis = true;
          return;
        }

        return;
      });

      return !hasReturnClassType && hasReturnThis;
    }
```
</details>

- **Parameters**:
  - `originalFunc: FunctionLike`
  - `originalClass: ClassLikeDeclaration`
- **Return Type**: `boolean`
- **Calls**:
  - `isThisSpecifiedInParameters`
  - `services.esTreeNodeToTSNodeMap.get`
  - `services.getTypeAtLocation`
  - `checker.getTypeAtLocation`
  - `forEachReturnStatement (from ../util)`
- **Internal Comments**:
```
// fast check
```

### `checkFunction(originalFunc: FunctionLike, originalClass: ClassLikeDeclaration): void`

<details><summary>Code</summary>

```ts
function checkFunction(
      originalFunc: FunctionLike,
      originalClass: ClassLikeDeclaration,
    ): void {
      const className = originalClass.id?.name;
      if (!className || !originalFunc.returnType) {
        return;
      }

      const node = tryGetNameInType(
        className,
        originalFunc.returnType.typeAnnotation,
      );
      if (!node) {
        return;
      }

      if (isFunctionReturningThis(originalFunc, originalClass)) {
        context.report({
          node,
          messageId: 'useThisType',
          fix: fixer => fixer.replaceText(node, 'this'),
        });
      }
    }
```
</details>

- **Parameters**:
  - `originalFunc: FunctionLike`
  - `originalClass: ClassLikeDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `tryGetNameInType`
  - `isFunctionReturningThis`
  - `context.report`
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'this')
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
fixer => fixer.replaceText(node, 'this')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `checkProperty(node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition): void`

<details><summary>Code</summary>

```ts
function checkProperty(
      node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition,
    ): void {
      if (
        !(
          node.value?.type === AST_NODE_TYPES.FunctionExpression ||
          node.value?.type === AST_NODE_TYPES.ArrowFunctionExpression
        )
      ) {
        return;
      }

      checkFunction(node.value, node.parent.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorProperty | TSESTree.PropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `checkFunction`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => fixer.replaceText(node, 'this')
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
fixer => fixer.replaceText(node, 'this')
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `ClassLikeDeclaration`

```ts
type ClassLikeDeclaration = | TSESTree.ClassDeclaration
  | TSESTree.ClassExpression;
```

### `FunctionLike`

```ts
type FunctionLike = | TSESTree.ArrowFunctionExpression
  | TSESTree.MethodDefinition['value'];
```


---