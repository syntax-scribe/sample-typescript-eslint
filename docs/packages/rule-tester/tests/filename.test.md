[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `filename.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/tests/filename.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `RuleTester` | `../src/RuleTester` |


---

## Functions

### `create(context: any): { Program(node: any): void; }`

<details><summary>Code</summary>

```ts
context => ({
    Program(node): void {
      context.report({
        node,
        messageId: 'foo',
        suggest:
          node.body.length === 1 &&
          node.body[0].type === AST_NODE_TYPES.EmptyStatement
            ? [
                {
                  messageId: 'createError',
                  fix(fixer): TSESLint.RuleFix {
                    return fixer.replaceText(node, '//');
                  },
                },
              ]
            : [],
      });
    },
  })
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(node: any): void; }`
### `create(context: any): { Program(node: any): void; }`

<details><summary>Code</summary>

```ts
context => ({
    Program(node): void {
      context.report({
        node,
        messageId: 'foo',
        suggest:
          node.body.length === 1 &&
          node.body[0].type === AST_NODE_TYPES.EmptyStatement
            ? [
                {
                  messageId: 'createError',
                  fix(fixer): TSESLint.RuleFix {
                    return fixer.replaceText(node, '//');
                  },
                },
              ]
            : [],
      });
    },
  })
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(node: any): void; }`
### `create(context: any): { Program(node: any): void; }`

<details><summary>Code</summary>

```ts
context => ({
    Program(node): void {
      context.report({
        node,
        messageId: 'foo',
        suggest:
          node.body.length === 1 &&
          node.body[0].type === AST_NODE_TYPES.EmptyStatement
            ? [
                {
                  messageId: 'createError',
                  fix(fixer): TSESLint.RuleFix {
                    return fixer.replaceText(node, '//');
                  },
                },
              ]
            : [],
      });
    },
  })
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(node: any): void; }`
### `create(context: any): { Program(node: any): void; }`

<details><summary>Code</summary>

```ts
context => ({
    Program(node): void {
      context.report({
        node,
        messageId: 'foo',
        suggest:
          node.body.length === 1 &&
          node.body[0].type === AST_NODE_TYPES.EmptyStatement
            ? [
                {
                  messageId: 'createError',
                  fix(fixer): TSESLint.RuleFix {
                    return fixer.replaceText(node, '//');
                  },
                },
              ]
            : [],
      });
    },
  })
```
</details>

- **Parameters**:
  - `context: any`
- **Return Type**: `{ Program(node: any): void; }`

---