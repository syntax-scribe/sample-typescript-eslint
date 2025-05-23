[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-invalid-void-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-invalid-void-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `hasOverloadSignatures` | `../util` |


---

## Functions

### `checkGenericTypeArgument(node: TSESTree.TSVoidKeyword): void`

<details><summary>Code</summary>

```ts
function checkGenericTypeArgument(node: TSESTree.TSVoidKeyword): void {
      // only matches T<..., void, ...>
      // extra check for precaution
      /* istanbul ignore next */
      if (
        node.parent.type !== AST_NODE_TYPES.TSTypeParameterInstantiation ||
        node.parent.parent.type !== AST_NODE_TYPES.TSTypeReference
      ) {
        return;
      }

      // check allowlist
      if (Array.isArray(allowInGenericTypeArguments)) {
        const fullyQualifiedName = context.sourceCode
          .getText(node.parent.parent.typeName)
          .replaceAll(' ', '');

        if (
          !allowInGenericTypeArguments
            .map(s => s.replaceAll(' ', ''))
            .includes(fullyQualifiedName)
        ) {
          context.report({
            node,
            messageId: 'invalidVoidForGeneric',
            data: { generic: fullyQualifiedName },
          });
        }
        return;
      }

      if (!allowInGenericTypeArguments) {
        context.report({
          node,
          messageId: allowAsThisParameter
            ? 'invalidVoidNotReturnOrThisParam'
            : 'invalidVoidNotReturn',
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @brief check if the given void keyword is used as a valid generic type
     *
     * reports if the type parametrized by void is not in the allowlist, or
     * allowInGenericTypeArguments is false.
     * no-op if the given void keyword is not used as generic type
     */
```

- **Parameters**:
  - `node: TSESTree.TSVoidKeyword`
- **Return Type**: `void`
- **Calls**:
  - `Array.isArray`
  - `context.sourceCode
          .getText(node.parent.parent.typeName)
          .replaceAll`
  - `allowInGenericTypeArguments
            .map(s => s.replaceAll(' ', ''))
            .includes`
  - `context.report`
- **Internal Comments**:
```
// only matches T<..., void, ...>
// extra check for precaution
/* istanbul ignore next */
// check allowlist
```

### `checkDefaultVoid(node: TSESTree.TSVoidKeyword, parentNode: TSESTree.TSTypeParameter): void`

<details><summary>Code</summary>

```ts
function checkDefaultVoid(
      node: TSESTree.TSVoidKeyword,
      parentNode: TSESTree.TSTypeParameter,
    ): void {
      if (parentNode.default !== node) {
        context.report({
          node,
          messageId: getNotReturnOrGenericMessageId(node),
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @brief checks if the generic type parameter defaults to void
     */
```

- **Parameters**:
  - `node: TSESTree.TSVoidKeyword`
  - `parentNode: TSESTree.TSTypeParameter`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getNotReturnOrGenericMessageId`
### `isValidUnionType(node: TSESTree.TSUnionType): boolean`

<details><summary>Code</summary>

```ts
function isValidUnionType(node: TSESTree.TSUnionType): boolean {
      return node.types.every(
        member =>
          validUnionMembers.includes(member.type) ||
          // allows any T<..., void, ...> here, checked by checkGenericTypeArgument
          (member.type === AST_NODE_TYPES.TSTypeReference &&
            member.typeArguments?.type ===
              AST_NODE_TYPES.TSTypeParameterInstantiation &&
            member.typeArguments.params
              .map(param => param.type)
              .includes(AST_NODE_TYPES.TSVoidKeyword)),
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @brief checks that a union containing void is valid
     * @return true if every member of the union is specified as a valid type in
     * validUnionMembers, or is a valid generic type parametrized by void
     */
```

- **Parameters**:
  - `node: TSESTree.TSUnionType`
- **Return Type**: `boolean`
- **Calls**:
  - `node.types.every`
  - `validUnionMembers.includes`
  - `member.typeArguments.params
              .map(param => param.type)
              .includes`
- **Internal Comments**:
```
// allows any T<..., void, ...> here, checked by checkGenericTypeArgument
```

### `getNotReturnOrGenericMessageId(node: TSESTree.TSVoidKeyword): MessageIds`

<details><summary>Code</summary>

```ts
function getNotReturnOrGenericMessageId(
  node: TSESTree.TSVoidKeyword,
): MessageIds {
  return node.parent.type === AST_NODE_TYPES.TSUnionType
    ? 'invalidVoidUnionConstituent'
    : 'invalidVoidNotReturnOrGeneric';
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSVoidKeyword`
- **Return Type**: `MessageIds`
### `getParentFunctionDeclarationNode(node: TSESTree.Node): TSESTree.FunctionDeclaration | TSESTree.MethodDefinition | null`

<details><summary>Code</summary>

```ts
function getParentFunctionDeclarationNode(
  node: TSESTree.Node,
): TSESTree.FunctionDeclaration | TSESTree.MethodDefinition | null {
  let current = node.parent;
  while (current) {
    if (current.type === AST_NODE_TYPES.FunctionDeclaration) {
      return current;
    }

    if (
      current.type === AST_NODE_TYPES.MethodDefinition &&
      current.value.body != null
    ) {
      return current;
    }

    current = current.parent;
  }

  return null;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.FunctionDeclaration | TSESTree.MethodDefinition | null`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `Options`

<details><summary>Interface Code</summary>

```ts
export interface Options {
  allowAsThisParameter?: boolean;
  allowInGenericTypeArguments?: boolean | [string, ...string[]];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowAsThisParameter` | `boolean` | ✓ |  |
| `allowInGenericTypeArguments` | `boolean | [string, ...string[]]` | ✓ |  |


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'invalidVoidForGeneric'
  | 'invalidVoidNotReturn'
  | 'invalidVoidNotReturnOrGeneric'
  | 'invalidVoidNotReturnOrThisParam'
  | 'invalidVoidNotReturnOrThisParamOrGeneric'
  | 'invalidVoidUnionConstituent';
```


---