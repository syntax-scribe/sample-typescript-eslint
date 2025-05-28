[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-declaration-merging.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 2 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-declaration-merging.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Scope` | `@typescript-eslint/scope-manager` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defs` | `any` | const | `variable.defs` | ✗ |
| `currentScope` | `any` | const | `context.sourceCode.getScope(node).upper` | ✗ |


---

## Functions

### `checkUnsafeDeclaration(scope: Scope, node: TSESTree.Identifier, unsafeKind: AST_NODE_TYPES): void`

<details><summary>Code</summary>

```ts
function checkUnsafeDeclaration(
      scope: Scope,
      node: TSESTree.Identifier,
      unsafeKind: AST_NODE_TYPES,
    ): void {
      const variable = scope.set.get(node.name);
      if (!variable) {
        return;
      }

      const defs = variable.defs;
      if (defs.length <= 1) {
        return;
      }

      if (defs.some(def => def.node.type === unsafeKind)) {
        context.report({
          node,
          messageId: 'unsafeMerging',
        });
      }
    }
```
</details>

- **Parameters**:
  - `scope: Scope`
  - `node: TSESTree.Identifier`
  - `unsafeKind: AST_NODE_TYPES`
- **Return Type**: `void`
- **Calls**:
  - `scope.set.get`
  - `defs.some`
  - `context.report`

---