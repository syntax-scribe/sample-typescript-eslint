[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-wrapper-object-types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `classNames` | `Set<string>` | const | `new Set([
  'BigInt',
  // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
  'Boolean',
  'Number',
  'Object',
  // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
  'String',
  'Symbol',
])` | ✗ |
| `typeName` | `any` | const | `node.type === AST_NODE_TYPES.Identifier && node.name` | ✗ |


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