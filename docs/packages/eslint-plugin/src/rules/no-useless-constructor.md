[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-useless-constructor.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 6 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-useless-constructor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `checkAccessibility(node: TSESTree.MethodDefinition): boolean`

<details><summary>Code</summary>

```ts
function checkAccessibility(node: TSESTree.MethodDefinition): boolean {
  switch (node.accessibility) {
    case 'protected':
    case 'private':
      return false;
    case 'public':
      if (node.parent.parent.superClass) {
        return false;
      }
      break;
  }
  return true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if method with accessibility is not useless
 */
```

- **Parameters**:
  - `node: TSESTree.MethodDefinition`
- **Return Type**: `boolean`
### `checkParams(node: TSESTree.MethodDefinition): boolean`

<details><summary>Code</summary>

```ts
function checkParams(node: TSESTree.MethodDefinition): boolean {
  return !node.value.params.some(
    param =>
      param.type === AST_NODE_TYPES.TSParameterProperty ||
      param.decorators.length,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if method is not useless due to typescript parameter properties and decorators
 */
```

- **Parameters**:
  - `node: TSESTree.MethodDefinition`
- **Return Type**: `boolean`
- **Calls**:
  - `node.value.params.some`

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