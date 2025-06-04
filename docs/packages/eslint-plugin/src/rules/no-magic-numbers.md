[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-magic-numbers.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 10 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 5 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-magic-numbers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `deepMerge` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `schema` | `JSONSchema4` | const | `deepMerge(
  // eslint-disable-next-line @typescript-eslint/no-unsafe-argument -- https://github.com/microsoft/TypeScript/issues/17002
  Array.isArray(baseRule.meta.schema)
    ? baseRule.meta.schema[0]
    : baseRule.meta.schema,
  {
    properties: {
      ignoreEnums: {
        type: 'boolean',
        description: 'Whether enums used in TypeScript are considered okay.',
      },
      ignoreNumericLiteralTypes: {
        type: 'boolean',
        description:
          'Whether numbers used in TypeScript numeric literal types are considered okay.',
      },
      ignoreReadonlyClassProperties: {
        type: 'boolean',
        description: 'Whether `readonly` class properties are considered okay.',
      },
      ignoreTypeIndexes: {
        type: 'boolean',
        description: 'Whether numbers used to index types are okay.',
      },
    },
  },
) as unknown as JSONSchema4` | ✗ |
| `ignored` | `Set<unknown>` | const | `new Set((options.ignore ?? []).map(normalizeIgnoreValue))` | ✗ |
| `isAllowed` | `boolean | undefined` | let/var | `*not shown*` | ✗ |
| `fullNumberNode` | `TSESTree.Literal | TSESTree.UnaryExpression` | let/var | `node` | ✗ |
| `raw` | `any` | let/var | `node.raw` | ✗ |


---

## Functions

### `normalizeIgnoreValue(value: bigint | number | string): bigint | number`

<details><summary>Code</summary>

```ts
function normalizeIgnoreValue(
  value: bigint | number | string,
): bigint | number {
  if (typeof value === 'string') {
    return BigInt(value.slice(0, -1));
  }

  return value;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert the value to bigint if it's a string. Otherwise, return the value as-is.
 * @param value The value to normalize.
 * @returns The normalized value.
 */
```

- **Parameters**:
  - `value: bigint | number | string`
- **Return Type**: `bigint | number`
- **Calls**:
  - `BigInt`
  - `value.slice`
### `normalizeLiteralValue(node: TSESTree.BigIntLiteral | TSESTree.NumberLiteral, value: bigint | number): bigint | number`

<details><summary>Code</summary>

```ts
function normalizeLiteralValue(
  node: TSESTree.BigIntLiteral | TSESTree.NumberLiteral,
  value: bigint | number,
): bigint | number {
  if (
    node.parent.type === AST_NODE_TYPES.UnaryExpression &&
    ['-', '+'].includes(node.parent.operator) &&
    node.parent.operator === '-'
  ) {
    return -value;
  }

  return value;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Converts the node to its numeric value, handling prefixed numbers (-1 / +1)
 * @param node the node to normalize.
 * @param value the node's value.
 */
```

- **Parameters**:
  - `node: TSESTree.BigIntLiteral | TSESTree.NumberLiteral`
  - `value: bigint | number`
- **Return Type**: `bigint | number`
- **Calls**:
  - `['-', '+'].includes`
### `getLiteralParent(node: TSESTree.Literal): TSESTree.Node | undefined`

<details><summary>Code</summary>

```ts
function getLiteralParent(node: TSESTree.Literal): TSESTree.Node | undefined {
  if (
    node.parent.type === AST_NODE_TYPES.UnaryExpression &&
    ['-', '+'].includes(node.parent.operator)
  ) {
    return node.parent.parent;
  }

  return node.parent;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the true parent of the literal, handling prefixed numbers (-1 / +1)
 */
```

- **Parameters**:
  - `node: TSESTree.Literal`
- **Return Type**: `TSESTree.Node | undefined`
- **Calls**:
  - `['-', '+'].includes`
### `isGrandparentTSTypeAliasDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isGrandparentTSTypeAliasDeclaration(node: TSESTree.Node): boolean {
  return node.parent?.parent?.type === AST_NODE_TYPES.TSTypeAliasDeclaration;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node grandparent is a Typescript type alias declaration
 * @param node the node to be validated.
 * @returns true if the node grandparent is a Typescript type alias declaration
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isGrandparentTSUnionType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isGrandparentTSUnionType(node: TSESTree.Node): boolean {
  if (node.parent?.parent?.type === AST_NODE_TYPES.TSUnionType) {
    return isGrandparentTSTypeAliasDeclaration(node.parent);
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node grandparent is a Typescript union type and its parent is a type alias declaration
 * @param node the node to be validated.
 * @returns true if the node grandparent is a Typescript union type and its parent is a type alias declaration
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isGrandparentTSTypeAliasDeclaration`
### `isParentTSEnumDeclaration(node: TSESTree.Literal): boolean`

<details><summary>Code</summary>

```ts
function isParentTSEnumDeclaration(node: TSESTree.Literal): boolean {
  const parent = getLiteralParent(node);
  return parent?.type === AST_NODE_TYPES.TSEnumMember;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node parent is a Typescript enum member
 * @param node the node to be validated.
 * @returns true if the node parent is a Typescript enum member
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Literal`
- **Return Type**: `boolean`
- **Calls**:
  - `getLiteralParent`
### `isParentTSLiteralType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isParentTSLiteralType(node: TSESTree.Node): boolean {
  return node.parent?.type === AST_NODE_TYPES.TSLiteralType;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node parent is a Typescript literal type
 * @param node the node to be validated.
 * @returns true if the node parent is a Typescript literal type
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isTSNumericLiteralType(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isTSNumericLiteralType(node: TSESTree.Node): boolean {
  // For negative numbers, use the parent node
  if (
    node.parent?.type === AST_NODE_TYPES.UnaryExpression &&
    node.parent.operator === '-'
  ) {
    node = node.parent;
  }

  // If the parent node is not a TSLiteralType, early return
  if (!isParentTSLiteralType(node)) {
    return false;
  }

  // If the grandparent is a TSTypeAliasDeclaration, ignore
  if (isGrandparentTSTypeAliasDeclaration(node)) {
    return true;
  }

  // If the grandparent is a TSUnionType and it's parent is a TSTypeAliasDeclaration, ignore
  if (isGrandparentTSUnionType(node)) {
    return true;
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node is a valid TypeScript numeric literal type.
 * @param node the node to be validated.
 * @returns true if the node is a TypeScript numeric literal type.
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isParentTSLiteralType`
  - `isGrandparentTSTypeAliasDeclaration`
  - `isGrandparentTSUnionType`
- **Internal Comments**:
```
// For negative numbers, use the parent node
// If the parent node is not a TSLiteralType, early return
// If the grandparent is a TSTypeAliasDeclaration, ignore
// If the grandparent is a TSUnionType and it's parent is a TSTypeAliasDeclaration, ignore
```

### `isParentTSReadonlyPropertyDefinition(node: TSESTree.Literal): boolean`

<details><summary>Code</summary>

```ts
function isParentTSReadonlyPropertyDefinition(node: TSESTree.Literal): boolean {
  const parent = getLiteralParent(node);

  if (parent?.type === AST_NODE_TYPES.PropertyDefinition && parent.readonly) {
    return true;
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node parent is a readonly class property
 * @param node the node to be validated.
 * @returns true if the node parent is a readonly class property
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Literal`
- **Return Type**: `boolean`
- **Calls**:
  - `getLiteralParent`
### `isAncestorTSIndexedAccessType(node: TSESTree.Literal): boolean`

<details><summary>Code</summary>

```ts
function isAncestorTSIndexedAccessType(node: TSESTree.Literal): boolean {
  // Handle unary expressions (eg. -4)
  let ancestor = getLiteralParent(node);

  // Go up another level while we’re part of a type union (eg. 1 | 2) or
  // intersection (eg. 1 & 2)
  while (
    ancestor?.parent?.type === AST_NODE_TYPES.TSUnionType ||
    ancestor?.parent?.type === AST_NODE_TYPES.TSIntersectionType
  ) {
    ancestor = ancestor.parent;
  }

  return ancestor?.parent?.type === AST_NODE_TYPES.TSIndexedAccessType;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the node is part of a type indexed access (eg. Foo[4])
 * @param node the node to be validated.
 * @returns true if the node is part of an indexed access
 * @private
 */
```

- **Parameters**:
  - `node: TSESTree.Literal`
- **Return Type**: `boolean`
- **Calls**:
  - `getLiteralParent`
- **Internal Comments**:
```
// Handle unary expressions (eg. -4) (x2)
// Go up another level while we’re part of a type union (eg. 1 | 2) or
// intersection (eg. 1 & 2)
```


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


---