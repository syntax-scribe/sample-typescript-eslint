[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-function-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-function-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isReferenceToGlobalFunction` | `../util` |


---

## Functions

### `checkBannedTypes(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function checkBannedTypes(node: TSESTree.Node): void {
      if (
        node.type === AST_NODE_TYPES.Identifier &&
        node.name === 'Function' &&
        isReferenceToGlobalFunction('Function', node, context.sourceCode)
      ) {
        context.report({
          node,
          messageId: 'bannedFunctionType',
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `isReferenceToGlobalFunction (from ../util)`
  - `context.report`

---