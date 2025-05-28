[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getForStatementHeadLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getForStatementHeadLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `nullThrows` | `@typescript-eslint/utils/eslint-utils` |


---

## Functions

### `getForStatementHeadLoc(sourceCode: TSESLint.SourceCode, node: | TSESTree.ForInStatement
    | TSESTree.ForOfStatement
    | TSESTree.ForStatement): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getForStatementHeadLoc(
  sourceCode: TSESLint.SourceCode,
  node:
    | TSESTree.ForInStatement
    | TSESTree.ForOfStatement
    | TSESTree.ForStatement,
): TSESTree.SourceLocation {
  const closingParens = nullThrows(
    sourceCode.getTokenBefore(node.body, token => token.value === ')'),
    'for statement must have a closing parenthesis.',
  );
  return {
    end: structuredClone(closingParens.loc.end),
    start: structuredClone(node.loc.start),
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the location of the head of the given for statement variant for reporting.
 *
 * - `for (const foo in bar) expressionOrBlock`
 *    ^^^^^^^^^^^^^^^^^^^^^^
 *
 * - `for (const foo of bar) expressionOrBlock`
 *    ^^^^^^^^^^^^^^^^^^^^^^
 *
 * - `for await (const foo of bar) expressionOrBlock`
 *    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 *
 * - `for (let i = 0; i < 10; i++) expressionOrBlock`
 *    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 */
```

- **Parameters**:
  - `sourceCode: TSESLint.SourceCode`
  - `node: | TSESTree.ForInStatement
    | TSESTree.ForOfStatement
    | TSESTree.ForStatement`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `nullThrows (from @typescript-eslint/utils/eslint-utils)`
  - `sourceCode.getTokenBefore`
  - `structuredClone`

---