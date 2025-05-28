[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `astUtils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 1 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/astUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `escapeRegExp` | `./escapeRegExp` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `namePattern` | `RegExp` | const | `new RegExp(
    `[\\s,]${escapeRegExp(name)}(?:$|[\\s,:])`,
    'gu',
  )` | ✗ |
| `end` | `{ column: any; line: any; }` | const | `{
    column: start.column + (match ? name.length : 1),
    line: start.line,
  }` | ✗ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| namespace | `@typescript-eslint/utils/ast-utils` | * |


---

## Functions

### `getNameLocationInGlobalDirectiveComment(sourceCode: TSESLint.SourceCode, comment: TSESTree.Comment, name: string): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getNameLocationInGlobalDirectiveComment(
  sourceCode: TSESLint.SourceCode,
  comment: TSESTree.Comment,
  name: string,
): TSESTree.SourceLocation {
  const namePattern = new RegExp(
    `[\\s,]${escapeRegExp(name)}(?:$|[\\s,:])`,
    'gu',
  );

  // To ignore the first text "global".
  namePattern.lastIndex = comment.value.indexOf('global') + 6;

  // Search a given variable name.
  const match = namePattern.exec(comment.value);

  // Convert the index to loc.
  const start = sourceCode.getLocFromIndex(
    comment.range[0] + '/*'.length + (match ? match.index + 1 : 0),
  );
  const end = {
    column: start.column + (match ? name.length : 1),
    line: start.line,
  };

  return { end, start };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Get the `loc` object of a given name in a `/*globals` directive comment.
 * @param sourceCode The source code to convert index to loc.
 * @param comment The `/*globals` directive comment which include the name.
 * @param name The name to find.
 * @returns The `loc` object.
 */
```

- **Parameters**:
  - `sourceCode: TSESLint.SourceCode`
  - `comment: TSESTree.Comment`
  - `name: string`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `escapeRegExp (from ./escapeRegExp)`
  - `comment.value.indexOf`
  - `namePattern.exec`
  - `sourceCode.getLocFromIndex`
- **Internal Comments**:
```
// To ignore the first text "global". (x4)
// Search a given variable name. (x2)
// Convert the index to loc. (x2)
```

### `forEachReturnStatement(body: ts.Block, visitor: (stmt: ts.ReturnStatement) => T): T | undefined`

<details><summary>Code</summary>

```ts
export function forEachReturnStatement<T>(
  body: ts.Block,
  visitor: (stmt: ts.ReturnStatement) => T,
): T | undefined {
  return traverse(body);

  function traverse(node: ts.Node): T | undefined {
    switch (node.kind) {
      case ts.SyntaxKind.ReturnStatement:
        return visitor(node as ts.ReturnStatement);
      case ts.SyntaxKind.CaseBlock:
      case ts.SyntaxKind.Block:
      case ts.SyntaxKind.IfStatement:
      case ts.SyntaxKind.DoStatement:
      case ts.SyntaxKind.WhileStatement:
      case ts.SyntaxKind.ForStatement:
      case ts.SyntaxKind.ForInStatement:
      case ts.SyntaxKind.ForOfStatement:
      case ts.SyntaxKind.WithStatement:
      case ts.SyntaxKind.SwitchStatement:
      case ts.SyntaxKind.CaseClause:
      case ts.SyntaxKind.DefaultClause:
      case ts.SyntaxKind.LabeledStatement:
      case ts.SyntaxKind.TryStatement:
      case ts.SyntaxKind.CatchClause:
        return ts.forEachChild(node, traverse);
    }

    return undefined;
  }
}
```
</details>

- **Parameters**:
  - `body: ts.Block`
  - `visitor: (stmt: ts.ReturnStatement) => T`
- **Return Type**: `T | undefined`
- **Calls**:
  - `traverse`
  - `visitor`
  - `ts.forEachChild`
### `traverse(node: ts.Node): T | undefined`

<details><summary>Code</summary>

```ts
function traverse(node: ts.Node): T | undefined {
    switch (node.kind) {
      case ts.SyntaxKind.ReturnStatement:
        return visitor(node as ts.ReturnStatement);
      case ts.SyntaxKind.CaseBlock:
      case ts.SyntaxKind.Block:
      case ts.SyntaxKind.IfStatement:
      case ts.SyntaxKind.DoStatement:
      case ts.SyntaxKind.WhileStatement:
      case ts.SyntaxKind.ForStatement:
      case ts.SyntaxKind.ForInStatement:
      case ts.SyntaxKind.ForOfStatement:
      case ts.SyntaxKind.WithStatement:
      case ts.SyntaxKind.SwitchStatement:
      case ts.SyntaxKind.CaseClause:
      case ts.SyntaxKind.DefaultClause:
      case ts.SyntaxKind.LabeledStatement:
      case ts.SyntaxKind.TryStatement:
      case ts.SyntaxKind.CatchClause:
        return ts.forEachChild(node, traverse);
    }

    return undefined;
  }
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `T | undefined`
- **Calls**:
  - `visitor`
  - `ts.forEachChild`

---