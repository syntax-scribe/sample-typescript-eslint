[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-dupe-class-members.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 2

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


---