[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-wrapper-object-types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-wrapper-object-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isReferenceToGlobalFunction` | `../util` |


---

## Functions

### `checkBannedTypes(node: TSESTree.EntityName | TSESTree.Expression, includeFix: boolean): void`

<details><summary>Code</summary>

```ts
function checkBannedTypes(
      node: TSESTree.EntityName | TSESTree.Expression,
      includeFix: boolean,
    ): void {
      const typeName = node.type === AST_NODE_TYPES.Identifier && node.name;
      if (
        !typeName ||
        !classNames.has(typeName) ||
        !isReferenceToGlobalFunction(typeName, node, context.sourceCode)
      ) {
        return;
      }

      const preferred = typeName.toLowerCase();

      context.report({
        node,
        messageId: 'bannedClassType',
        data: { preferred, typeName },
        fix: includeFix
          ? (fixer): TSESLint.RuleFix => fixer.replaceText(node, preferred)
          : undefined,
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.EntityName | TSESTree.Expression`
  - `includeFix: boolean`
- **Return Type**: `void`
- **Calls**:
  - `classNames.has`
  - `isReferenceToGlobalFunction (from ../util)`
  - `typeName.toLowerCase`
  - `context.report`
  - `fixer.replaceText`

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