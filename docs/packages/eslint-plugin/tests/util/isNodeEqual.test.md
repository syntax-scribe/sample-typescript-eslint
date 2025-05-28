[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isNodeEqual.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |


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