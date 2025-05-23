[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isNodeEqual.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/util/isNodeEqual.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `createRule` | `../../src/util` |
| `isNodeEqual` | `../../src/util` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Functions

### `LogicalExpression(node: TSESTree.LogicalExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.LogicalExpression): void => {
        if (isNodeEqual(node.left, node.right)) {
          context.report({
            fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix {
              return fixer.replaceText(
                node,
                context.sourceCode.text.slice(
                  node.left.range[0],
                  node.left.range[1],
                ),
              );
            },
            messageId: 'removeExpression',
            node,
          });
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `void`
- **Calls**:
  - `isNodeEqual (from ../../src/util)`
  - `context.report`
  - `fixer.replaceText`
  - `context.sourceCode.text.slice`
### `LogicalExpression(node: TSESTree.LogicalExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.LogicalExpression): void => {
        if (isNodeEqual(node.left, node.right)) {
          context.report({
            fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix {
              return fixer.replaceText(
                node,
                context.sourceCode.text.slice(
                  node.left.range[0],
                  node.left.range[1],
                ),
              );
            },
            messageId: 'removeExpression',
            node,
          });
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `void`
- **Calls**:
  - `isNodeEqual (from ../../src/util)`
  - `context.report`
  - `fixer.replaceText`
  - `context.sourceCode.text.slice`
### `LogicalExpression(node: TSESTree.LogicalExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.LogicalExpression): void => {
        if (isNodeEqual(node.left, node.right)) {
          context.report({
            fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix {
              return fixer.replaceText(
                node,
                context.sourceCode.text.slice(
                  node.left.range[0],
                  node.left.range[1],
                ),
              );
            },
            messageId: 'removeExpression',
            node,
          });
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `void`
- **Calls**:
  - `isNodeEqual (from ../../src/util)`
  - `context.report`
  - `fixer.replaceText`
  - `context.sourceCode.text.slice`
### `LogicalExpression(node: TSESTree.LogicalExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.LogicalExpression): void => {
        if (isNodeEqual(node.left, node.right)) {
          context.report({
            fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix {
              return fixer.replaceText(
                node,
                context.sourceCode.text.slice(
                  node.left.range[0],
                  node.left.range[1],
                ),
              );
            },
            messageId: 'removeExpression',
            node,
          });
        }
      }
```
</details>

- **Parameters**:
  - `node: TSESTree.LogicalExpression`
- **Return Type**: `void`
- **Calls**:
  - `isNodeEqual (from ../../src/util)`
  - `context.report`
  - `fixer.replaceText`
  - `context.sourceCode.text.slice`

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