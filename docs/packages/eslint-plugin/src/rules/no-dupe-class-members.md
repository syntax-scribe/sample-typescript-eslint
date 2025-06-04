[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-dupe-class-members.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 6 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-dupe-class-members.ts`**

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

### `wrapMemberDefinitionListener(coreListener: (node: N) => void): (node: N) => void`

<details><summary>Code</summary>

```ts
function wrapMemberDefinitionListener<
      N extends TSESTree.MethodDefinition | TSESTree.PropertyDefinition,
    >(coreListener: (node: N) => void): (node: N) => void {
      return (node: N): void => {
        if (node.computed) {
          return;
        }

        if (
          node.value &&
          node.value.type === AST_NODE_TYPES.TSEmptyBodyFunctionExpression
        ) {
          return;
        }

        return coreListener(node);
      };
    }
```
</details>

- **Parameters**:
  - `coreListener: (node: N) => void`
- **Return Type**: `(node: N) => void`
- **Calls**:
  - `coreListener`

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