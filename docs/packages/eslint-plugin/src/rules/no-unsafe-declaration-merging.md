[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-declaration-merging.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---