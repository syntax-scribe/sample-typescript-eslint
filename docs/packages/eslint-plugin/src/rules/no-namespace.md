[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-namespace.ts`

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
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-namespace.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isDefinitionFile` | `../util` |


---

## Functions

### `isDeclaration(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isDeclaration(node: TSESTree.Node): boolean {
      if (node.type === AST_NODE_TYPES.TSModuleDeclaration && node.declare) {
        return true;
      }

      return node.parent != null && isDeclaration(node.parent);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isDeclaration`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowDeclarations?: boolean;
    allowDefinitionFiles?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'moduleSyntaxIsPreferred';
```


---