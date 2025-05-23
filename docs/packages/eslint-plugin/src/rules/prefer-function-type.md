[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-function-type.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-function-type.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `hasOneSupertype(node: TSESTree.TSInterfaceDeclaration): boolean`

<details><summary>Code</summary>

```ts
function hasOneSupertype(node: TSESTree.TSInterfaceDeclaration): boolean {
      if (node.extends.length === 0) {
        return false;
      }
      if (node.extends.length !== 1) {
        return true;
      }
      const expr = node.extends[0].expression;

      return (
        expr.type !== AST_NODE_TYPES.Identifier || expr.name !== 'Function'
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if there the interface has exactly one supertype that isn't named 'Function'
     * @param node The node being checked
     */
```

- **Parameters**:
  - `node: TSESTree.TSInterfaceDeclaration`
- **Return Type**: `boolean`
### `shouldWrapSuggestion(parent: TSESTree.Node | undefined): boolean`

<details><summary>Code</summary>

```ts
function shouldWrapSuggestion(parent: TSESTree.Node | undefined): boolean {
      if (!parent) {
        return false;
      }

      switch (parent.type) {
        case AST_NODE_TYPES.TSUnionType:
        case AST_NODE_TYPES.TSIntersectionType:
        case AST_NODE_TYPES.TSArrayType:
          return true;
        default:
          return false;
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param parent The parent of the call signature causing the diagnostic
     */
```

- **Parameters**:
  - `parent: TSESTree.Node | undefined`
- **Return Type**: `boolean`
### `checkMember(member: TSESTree.TypeElement, node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral, tsThisTypes: TSESTree.TSThisType[] | null): void`

<details><summary>Code</summary>

```ts
function checkMember(
      member: TSESTree.TypeElement,
      node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral,
      tsThisTypes: TSESTree.TSThisType[] | null = null,
    ): void {
      if (
        (member.type === AST_NODE_TYPES.TSCallSignatureDeclaration ||
          member.type === AST_NODE_TYPES.TSConstructSignatureDeclaration) &&
        member.returnType != null
      ) {
        if (
          tsThisTypes?.length &&
          node.type === AST_NODE_TYPES.TSInterfaceDeclaration
        ) {
          // the message can be confusing if we don't point directly to the `this` node instead of the whole member
          // and in favour of generating at most one error we'll only report the first occurrence of `this` if there are multiple
          context.report({
            node: tsThisTypes[0],
            messageId: 'unexpectedThisOnFunctionOnlyInterface',
            data: {
              interfaceName: node.id.name,
            },
          });
          return;
        }

        const fixable =
          node.parent.type === AST_NODE_TYPES.ExportDefaultDeclaration;

        const fix = fixable
          ? null
          : (fixer: TSESLint.RuleFixer): TSESLint.RuleFix[] => {
              const fixes: TSESLint.RuleFix[] = [];
              const start = member.range[0];
              // https://github.com/microsoft/TypeScript/pull/56908
              // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
              const colonPos = member.returnType!.range[0] - start;
              const text = context.sourceCode
                .getText()
                .slice(start, member.range[1]);
              const comments = [
                ...context.sourceCode.getCommentsBefore(member),
                ...context.sourceCode.getCommentsAfter(member),
              ];
              let suggestion = `${text.slice(0, colonPos)} =>${text.slice(
                colonPos + 1,
              )}`;
              const lastChar = suggestion.endsWith(';') ? ';' : '';
              if (lastChar) {
                suggestion = suggestion.slice(0, -1);
              }
              if (shouldWrapSuggestion(node.parent)) {
                suggestion = `(${suggestion})`;
              }

              if (node.type === AST_NODE_TYPES.TSInterfaceDeclaration) {
                if (node.typeParameters != null) {
                  suggestion = `type ${context.sourceCode
                    .getText()
                    .slice(
                      node.id.range[0],
                      node.typeParameters.range[1],
                    )} = ${suggestion}${lastChar}`;
                } else {
                  suggestion = `type ${node.id.name} = ${suggestion}${lastChar}`;
                }
              }

              const isParentExported =
                node.parent.type === AST_NODE_TYPES.ExportNamedDeclaration;

              if (
                node.type === AST_NODE_TYPES.TSInterfaceDeclaration &&
                isParentExported
              ) {
                const commentsText = comments
                  .map(({ type, value }) =>
                    type === AST_TOKEN_TYPES.Line
                      ? `//${value}\n`
                      : `/*${value}*/\n`,
                  )
                  .join('');
                // comments should move before export and not between export and interface declaration
                fixes.push(fixer.insertTextBefore(node.parent, commentsText));
              } else {
                comments.forEach(comment => {
                  let commentText =
                    comment.type === AST_TOKEN_TYPES.Line
                      ? `//${comment.value}`
                      : `/*${comment.value}*/`;
                  const isCommentOnTheSameLine =
                    comment.loc.start.line === member.loc.start.line;
                  if (!isCommentOnTheSameLine) {
                    commentText += '\n';
                  } else {
                    commentText += ' ';
                  }
                  suggestion = commentText + suggestion;
                });
              }

              const fixStart = node.range[0];
              fixes.push(
                fixer.replaceTextRange([fixStart, node.range[1]], suggestion),
              );
              return fixes;
            };

        context.report({
          node: member,
          messageId: 'functionTypeOverCallableType',
          data: {
            literalOrInterface: phrases[node.type],
          },
          fix,
        });
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @param member The TypeElement being checked
     * @param node The parent of member being checked
     */
```

- **Parameters**:
  - `member: TSESTree.TypeElement`
  - `node: TSESTree.TSInterfaceDeclaration | TSESTree.TSTypeLiteral`
  - `tsThisTypes: TSESTree.TSThisType[] | null`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `context.sourceCode
                .getText()
                .slice`
  - `context.sourceCode.getCommentsBefore`
  - `context.sourceCode.getCommentsAfter`
  - `text.slice`
  - `suggestion.endsWith`
  - `suggestion.slice`
  - `shouldWrapSuggestion`
  - `context.sourceCode
                    .getText()
                    .slice`
  - `comments
                  .map(({ type, value }) =>
                    type === AST_TOKEN_TYPES.Line
                      ? `//${value}\n`
                      : `/*${value}*/\n`,
                  )
                  .join`
  - `fixes.push`
  - `fixer.insertTextBefore`
  - `comments.forEach`
  - `fixer.replaceTextRange`
- **Internal Comments**:
```
// the message can be confusing if we don't point directly to the `this` node instead of the whole member (x4)
// and in favour of generating at most one error we'll only report the first occurrence of `this` if there are multiple (x4)
// https://github.com/microsoft/TypeScript/pull/56908 (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
// comments should move before export and not between export and interface declaration (x4)
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