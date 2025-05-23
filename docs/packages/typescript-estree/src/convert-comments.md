[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `convert-comments.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/convert-comments.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `./ts-estree` |
| `getLocFor` | `./node-utils` |
| `AST_TOKEN_TYPES` | `./ts-estree` |


---

## Functions

### `convertComments(ast: ts.SourceFile, code: string): TSESTree.Comment[]`

<details><summary>Code</summary>

```ts
export function convertComments(
  ast: ts.SourceFile,
  code: string,
): TSESTree.Comment[] {
  const comments: TSESTree.Comment[] = [];

  tsutils.forEachComment(
    ast,
    (_, comment) => {
      const type =
        comment.kind === ts.SyntaxKind.SingleLineCommentTrivia
          ? AST_TOKEN_TYPES.Line
          : AST_TOKEN_TYPES.Block;
      const range: TSESTree.Range = [comment.pos, comment.end];
      const loc = getLocFor(range, ast);

      // both comments start with 2 characters - /* or //
      const textStart = range[0] + 2;
      const textEnd =
        comment.kind === ts.SyntaxKind.SingleLineCommentTrivia
          ? // single line comments end at the end
            range[1] - textStart
          : // multiline comments end 2 characters early
            range[1] - textStart - 2;
      comments.push({
        type,
        loc,
        range,
        value: code.slice(textStart, textStart + textEnd),
      });
    },
    ast,
  );

  return comments;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert all comments for the given AST.
 * @param ast the AST object
 * @param code the TypeScript code
 * @returns the converted ESTreeComment
 * @private
 */
```

- **Parameters**:
  - `ast: ts.SourceFile`
  - `code: string`
- **Return Type**: `TSESTree.Comment[]`
- **Calls**:
  - `tsutils.forEachComment`
  - `getLocFor (from ./node-utils)`
  - `comments.push`
  - `code.slice`
- **Internal Comments**:
```
// both comments start with 2 characters - /* or // (x2)
```


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