[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-extra-non-null-assertion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-extra-non-null-assertion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `checkExtraNonNullAssertion(node: TSESTree.TSNonNullExpression): void`

<details><summary>Code</summary>

```ts
function checkExtraNonNullAssertion(
      node: TSESTree.TSNonNullExpression,
    ): void {
      context.report({
        node,
        messageId: 'noExtraNonNullAssertion',
        fix(fixer) {
          return fixer.removeRange([node.range[1] - 1, node.range[1]]);
        },
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSNonNullExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `fixer.removeRange`

---