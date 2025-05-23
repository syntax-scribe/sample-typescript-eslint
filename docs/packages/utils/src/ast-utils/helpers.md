[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `helpers.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/helpers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../ts-estree` |
| `AST_TOKEN_TYPES` | `../ts-estree` |
| `TSESTree` | `../ts-estree` |


---

## Functions

### `isNodeOfType(nodeType: NodeType): (node: any) => node is any`

<details><summary>Code</summary>

```ts
<NodeType extends AST_NODE_TYPES>(nodeType: NodeType) =>
  (
    node: TSESTree.Node | null | undefined,
  ): node is Extract<TSESTree.Node, { type: NodeType }> =>
    node?.type === nodeType
```
</details>

- **Parameters**:
  - `nodeType: NodeType`
- **Return Type**: `(node: any) => node is any`
### `isNodeOfTypes(nodeTypes: NodeTypes): (node: any) => node is any`

<details><summary>Code</summary>

```ts
<NodeTypes extends readonly AST_NODE_TYPES[]>(nodeTypes: NodeTypes) =>
  (
    node: TSESTree.Node | null | undefined,
  ): node is Extract<TSESTree.Node, { type: NodeTypes[number] }> =>
    !!node && nodeTypes.includes(node.type)
```
</details>

- **Parameters**:
  - `nodeTypes: NodeTypes`
- **Return Type**: `(node: any) => node is any`
### `isNodeOfTypeWithConditions(nodeType: NodeType, conditions: Conditions): ((
  node: TSESTree.Node | null | undefined,
) => node is Conditions & ExtractedNode)`

<details><summary>Code</summary>

```ts
<
  NodeType extends AST_NODE_TYPES,
  ExtractedNode extends Extract<TSESTree.Node, { type: NodeType }>,
  Conditions extends Partial<ExtractedNode>,
>(
  nodeType: NodeType,
  conditions: Conditions,
): ((
  node: TSESTree.Node | null | undefined,
) => node is Conditions & ExtractedNode) => {
  const entries = Object.entries(conditions) as ObjectEntries<TSESTree.Node>;

  return (
    node: TSESTree.Node | null | undefined,
  ): node is Conditions & ExtractedNode =>
    node?.type === nodeType &&
    entries.every(([key, value]) => node[key as keyof TSESTree.Node] === value);
}
```
</details>

- **Parameters**:
  - `nodeType: NodeType`
  - `conditions: Conditions`
- **Return Type**: `((
  node: TSESTree.Node | null | undefined,
) => node is Conditions & ExtractedNode)`
- **Calls**:
  - `Object.entries`
  - `entries.every`
### `isTokenOfTypeWithConditions(tokenType: TokenType, conditions: Conditions): ((
  token: TSESTree.Token | null | undefined,
) => token is Conditions & ExtractedToken)`

<details><summary>Code</summary>

```ts
<
  TokenType extends AST_TOKEN_TYPES,
  // This is technically unsafe, but we find it useful to extract out the type
  // eslint-disable-next-line @typescript-eslint/no-unnecessary-type-parameters
  ExtractedToken extends Extract<TSESTree.Token, { type: TokenType }>,
  Conditions extends Partial<{ type: TokenType } & TSESTree.Token>,
>(
  tokenType: TokenType,
  conditions: Conditions,
): ((
  token: TSESTree.Token | null | undefined,
) => token is Conditions & ExtractedToken) => {
  const entries = Object.entries(conditions) as ObjectEntries<TSESTree.Token>;

  return (
    token: TSESTree.Token | null | undefined,
  ): token is Conditions & ExtractedToken =>
    token?.type === tokenType &&
    entries.every(
      ([key, value]) => token[key as keyof TSESTree.Token] === value,
    );
}
```
</details>

- **Parameters**:
  - `tokenType: TokenType`
  - `conditions: Conditions`
- **Return Type**: `((
  token: TSESTree.Token | null | undefined,
) => token is Conditions & ExtractedToken)`
- **Calls**:
  - `Object.entries`
  - `entries.every`
### `isNotTokenOfTypeWithConditions(tokenType: TokenType, conditions: Conditions): ((
    token: TSESTree.Token | null | undefined,
  ) => token is Exclude<TSESTree.Token, Conditions & ExtractedToken>)`

<details><summary>Code</summary>

```ts
<
    TokenType extends AST_TOKEN_TYPES,
    ExtractedToken extends Extract<TSESTree.Token, { type: TokenType }>,
    Conditions extends Partial<ExtractedToken>,
  >(
    tokenType: TokenType,
    conditions: Conditions,
  ): ((
    token: TSESTree.Token | null | undefined,
  ) => token is Exclude<TSESTree.Token, Conditions & ExtractedToken>) =>
  (token): token is Exclude<TSESTree.Token, Conditions & ExtractedToken> =>
    !isTokenOfTypeWithConditions(tokenType, conditions)(token)
```
</details>

- **Parameters**:
  - `tokenType: TokenType`
  - `conditions: Conditions`
- **Return Type**: `((
    token: TSESTree.Token | null | undefined,
  ) => token is Exclude<TSESTree.Token, Conditions & ExtractedToken>)`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `ObjectEntry<BaseType>`

```ts
type ObjectEntry<BaseType> = BaseType extends unknown
  ? [keyof BaseType, BaseType[keyof BaseType]]
  : never;
```

### `ObjectEntries<BaseType>`

```ts
type ObjectEntries<BaseType> = ObjectEntry<BaseType>[];
```


---