[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `related-getter-setter-pairs.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/related-getter-setter-pairs.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getNameFromMember` | `../util` |
| `getParserServices` | `../util` |


---

## Functions

### `addPropertyNode(member: GetMethod | SetMethod, inner: TSESTree.Node, kind: 'get' | 'set'): void`

<details><summary>Code</summary>

```ts
function addPropertyNode(
      member: GetMethod | SetMethod,
      inner: TSESTree.Node,
      kind: 'get' | 'set',
    ): void {
      const methodPairs = methodPairsStack[methodPairsStack.length - 1];
      const { name } = getNameFromMember(member, context.sourceCode);

      methodPairs.set(name, {
        ...methodPairs.get(name),
        [kind]: inner,
      });
    }
```
</details>

- **Parameters**:
  - `member: GetMethod | SetMethod`
  - `inner: TSESTree.Node`
  - `kind: 'get' | 'set'`
- **Return Type**: `void`
- **Calls**:
  - `getNameFromMember (from ../util)`
  - `methodPairs.set`
  - `methodPairs.get`
### `getMethodFromNode(node: GetMethodRaw | SetMethod): any`

<details><summary>Code</summary>

```ts
function getMethodFromNode(node: GetMethodRaw | SetMethod) {
  return node.type === AST_NODE_TYPES.TSMethodSignature ? node : node.value;
}
```
</details>

- **Parameters**:
  - `node: GetMethodRaw | SetMethod`
- **Return Type**: `any`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `MethodPair`

<details><summary>Interface Code</summary>

```ts
interface MethodPair {
  get?: GetMethod;
  set?: SetMethod;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `get` | `GetMethod` | ✓ |  |
| `set` | `SetMethod` | ✓ |  |


---

## Type Aliases

### `Method`

```ts
type Method = TSESTree.MethodDefinition | TSESTree.TSMethodSignature;
```

### `GetMethod`

```ts
type GetMethod = {
  kind: 'get';
  returnType: TSESTree.TSTypeAnnotation;
} & Method;
```

### `GetMethodRaw`

```ts
type GetMethodRaw = {
  returnType: TSESTree.TSTypeAnnotation | undefined;
} & GetMethod;
```

### `SetMethod`

```ts
type SetMethod = { kind: 'set'; params: [TSESTree.Node] } & Method;
```


---