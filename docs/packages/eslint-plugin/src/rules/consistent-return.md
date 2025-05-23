[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-return.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-return.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `isTypeFlagSet` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `enterFunction(node: FunctionNode): void`

<details><summary>Code</summary>

```ts
function enterFunction(node: FunctionNode): void {
      functions.push(node);
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `void`
- **Calls**:
  - `functions.push`
### `exitFunction(): void`

<details><summary>Code</summary>

```ts
function exitFunction(): void {
      functions.pop();
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `functions.pop`
### `getCurrentFunction(): FunctionNode | null`

<details><summary>Code</summary>

```ts
function getCurrentFunction(): FunctionNode | null {
      return functions[functions.length - 1] ?? null;
    }
```
</details>

- **Return Type**: `FunctionNode | null`
### `isPromiseVoid(node: ts.Node, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isPromiseVoid(node: ts.Node, type: ts.Type): boolean {
      if (
        tsutils.isThenableType(checker, node, type) &&
        tsutils.isTypeReference(type)
      ) {
        const awaitedType = type.typeArguments?.[0];
        if (awaitedType) {
          if (isTypeFlagSet(awaitedType, ts.TypeFlags.Void)) {
            return true;
          }
          return isPromiseVoid(node, awaitedType);
        }
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.isThenableType`
  - `tsutils.isTypeReference`
  - `isTypeFlagSet (from ../util)`
  - `isPromiseVoid`
### `isReturnVoidOrThenableVoid(node: FunctionNode): boolean`

<details><summary>Code</summary>

```ts
function isReturnVoidOrThenableVoid(node: FunctionNode): boolean {
      const functionType = services.getTypeAtLocation(node);
      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      const callSignatures = functionType.getCallSignatures();

      return callSignatures.some(signature => {
        const returnType = signature.getReturnType();
        if (node.async) {
          return isPromiseVoid(tsNode, returnType);
        }
        return isTypeFlagSet(returnType, ts.TypeFlags.Void);
      });
    }
```
</details>

- **Parameters**:
  - `node: FunctionNode`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getTypeAtLocation`
  - `services.esTreeNodeToTSNodeMap.get`
  - `functionType.getCallSignatures`
  - `callSignatures.some`
  - `signature.getReturnType`
  - `isPromiseVoid`
  - `isTypeFlagSet (from ../util)`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```

### `FunctionNode`

```ts
type FunctionNode = | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression;
```


---