[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-extra-non-null-assertion.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---