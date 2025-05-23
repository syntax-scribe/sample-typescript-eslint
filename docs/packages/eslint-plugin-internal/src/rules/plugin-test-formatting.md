[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `plugin-test-formatting.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 15
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/plugin-test-formatting.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `prettier` | `@prettier/sync` |
| `getContextualType` | `@typescript-eslint/type-utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `getExpectedIndentForNode(node: TSESTree.Node, sourceCodeLines: string[]): number`

<details><summary>Code</summary>

```ts
function getExpectedIndentForNode(
  node: TSESTree.Node,
  sourceCodeLines: string[],
): number {
  const lineIdx = node.loc.start.line - 1;
  // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
  const indent = START_OF_LINE_WHITESPACE_MATCHER.exec(
    sourceCodeLines[lineIdx],
  )![1];
  return indent.length;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `sourceCodeLines: string[]`
- **Return Type**: `number`
- **Calls**:
  - `START_OF_LINE_WHITESPACE_MATCHER.exec`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `doIndent(line: string, indent: number): string`

<details><summary>Code</summary>

```ts
function doIndent(line: string, indent: number): string {
  for (let i = 0; i < indent; i += 1) {
    line = ` ${line}`;
  }
  return line;
}
```
</details>

- **Parameters**:
  - `line: string`
  - `indent: number`
- **Return Type**: `string`
### `getQuote(code: string): "'" | '"' | null`

<details><summary>Code</summary>

```ts
function getQuote(code: string): "'" | '"' | null {
  const hasSingleQuote = code.includes("'");
  const hasDoubleQuote = code.includes('"');
  if (hasSingleQuote && hasDoubleQuote) {
    // be lazy and make them fix and escape the quotes manually
    return null;
  }

  return hasSingleQuote ? '"' : "'";
}
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `"'" | '"' | null`
- **Calls**:
  - `code.includes`
- **Internal Comments**:
```
// be lazy and make them fix and escape the quotes manually
```

### `escapeTemplateString(code: string): string`

<details><summary>Code</summary>

```ts
function escapeTemplateString(code: string): string {
  let fixed = code;
  fixed = fixed.replaceAll(BACKTICK_REGEX, '\\`');
  fixed = fixed.replaceAll(TEMPLATE_EXPR_OPENER, '\\${');
  return fixed;
}
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
- **Calls**:
  - `fixed.replaceAll`
### `getCodeFormatted(code: string): string | FormattingError`

<details><summary>Code</summary>

```ts
function getCodeFormatted(code: string): string | FormattingError {
      try {
        return prettier
          .format(code, {
            ...prettierConfig,
            parser: 'typescript',
          })
          .trimEnd(); // prettier will insert a new line at the end of the code
      } catch (ex) {
        // ex instanceof Error is false as of @prettier/sync@0.3.0, as is ex instanceof SyntaxError
        if (
          // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
          (ex as Partial<Error> | undefined)?.constructor?.name !==
          'SyntaxError'
        ) {
          throw ex;
        }

        return ex as FormattingError;
      }
    }
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string | FormattingError`
- **Calls**:
  - `prettier
          .format(code, {
            ...prettierConfig,
            parser: 'typescript',
          })
          .trimEnd`
- **Internal Comments**:
```
// ex instanceof Error is false as of @prettier/sync@0.3.0, as is ex instanceof SyntaxError
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition (x4)
```

### `getCodeFormattedOrReport(code: string, location: TSESTree.Node): string | null`

<details><summary>Code</summary>

```ts
function getCodeFormattedOrReport(
      code: string,
      location: TSESTree.Node,
    ): string | null {
      if (formatWithPrettier === false) {
        return null;
      }

      const formatted = getCodeFormatted(code);
      if (typeof formatted === 'string') {
        return formatted;
      }

      let message = formatted.message;

      if (formatted.codeFrame) {
        message = message.replace(`\n${formatted.codeFrame}`, '');
      }
      if (formatted.loc) {
        message = message.replace(/ \(\d+:\d+\)$/, '');
      }

      context.report({
        node: location,
        messageId: 'prettierException',
        data: {
          message,
        },
      });
      return null;
    }
```
</details>

- **Parameters**:
  - `code: string`
  - `location: TSESTree.Node`
- **Return Type**: `string | null`
- **Calls**:
  - `getCodeFormatted`
  - `message.replace`
  - `context.report`
### `checkExpression(node: TSESTree.Node | null, isErrorTest: boolean): void`

<details><summary>Code</summary>

```ts
function checkExpression(
      node: TSESTree.Node | null,
      isErrorTest: boolean,
    ): void {
      switch (node?.type) {
        case AST_NODE_TYPES.Literal:
          checkLiteral(node, isErrorTest);
          break;

        case AST_NODE_TYPES.TemplateLiteral:
          checkTemplateLiteral(node, isErrorTest);
          break;

        case AST_NODE_TYPES.TaggedTemplateExpression:
          checkTaggedTemplateExpression(node, isErrorTest);
          break;

        case AST_NODE_TYPES.CallExpression:
          checkCallExpression(node, isErrorTest);
          break;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null`
  - `isErrorTest: boolean`
- **Return Type**: `void`
- **Calls**:
  - `checkLiteral`
  - `checkTemplateLiteral`
  - `checkTaggedTemplateExpression`
  - `checkCallExpression`
### `checkLiteral(literal: TSESTree.Literal, isErrorTest: boolean, quoteIn: string): void`

<details><summary>Code</summary>

```ts
function checkLiteral(
      literal: TSESTree.Literal,
      isErrorTest: boolean,
      quoteIn?: string,
    ): void {
      if (typeof literal.value === 'string') {
        const output = getCodeFormattedOrReport(literal.value, literal);
        if (output && output !== literal.value) {
          context.report({
            node: literal,
            messageId: isErrorTest
              ? 'invalidFormattingErrorTest'
              : 'invalidFormatting',
            fix(fixer) {
              if (output.includes('\n')) {
                // formatted string is multiline, then have to use backticks
                return fixer.replaceText(
                  literal,
                  `\`${escapeTemplateString(output)}\``,
                );
              }

              const quote = quoteIn ?? getQuote(output);
              if (quote == null) {
                return null;
              }

              return fixer.replaceText(literal, `${quote}${output}${quote}`);
            },
          });
        }
      }
    }
```
</details>

- **Parameters**:
  - `literal: TSESTree.Literal`
  - `isErrorTest: boolean`
  - `quoteIn: string`
- **Return Type**: `void`
- **Calls**:
  - `getCodeFormattedOrReport`
  - `context.report`
  - `output.includes`
  - `fixer.replaceText`
  - `escapeTemplateString`
  - `getQuote`
- **Internal Comments**:
```
// formatted string is multiline, then have to use backticks
```

### `checkTemplateLiteral(literal: TSESTree.TemplateLiteral, isErrorTest: boolean, isNoFormatTagged: boolean): void`

<details><summary>Code</summary>

```ts
function checkTemplateLiteral(
      literal: TSESTree.TemplateLiteral,
      isErrorTest: boolean,
      isNoFormatTagged = false,
    ): void {
      if (literal.quasis.length > 1) {
        // ignore template literals with ${expressions} for simplicity
        return;
      }

      const text = literal.quasis[0].value.cooked;

      if (literal.loc.end.line === literal.loc.start.line) {
        // don't use template strings for single line tests
        return context.report({
          node: literal,
          messageId: 'singleLineQuotes',
          fix(fixer) {
            const quote = getQuote(text);
            if (quote == null) {
              return null;
            }

            return [
              fixer.replaceTextRange(
                [literal.range[0], literal.range[0] + 1],
                quote,
              ),
              fixer.replaceTextRange(
                [literal.range[1] - 1, literal.range[1]],
                quote,
              ),
            ];
          },
        });
      }

      const lines = text.split('\n');
      const lastLine = lines[lines.length - 1];
      // prettier will trim out the end of line on save, but eslint will check before then
      const isStartEmpty = lines[0].trimEnd() === '';
      // last line can be indented
      const isEndEmpty = lastLine.trimStart() === '';
      if (!isStartEmpty || !isEndEmpty) {
        // multiline template strings must have an empty first/last line
        return context.report({
          node: literal,
          messageId: 'templateLiteralEmptyEnds',
          *fix(fixer) {
            if (!isStartEmpty) {
              yield fixer.replaceTextRange(
                [literal.range[0], literal.range[0] + 1],
                '`\n',
              );
            }

            if (!isEndEmpty) {
              yield fixer.replaceTextRange(
                [literal.range[1] - 1, literal.range[1]],
                '\n`',
              );
            }
          },
        });
      }

      const parentIndent = getExpectedIndentForNode(
        literal,
        context.sourceCode.lines,
      );
      if (lastLine.length !== parentIndent) {
        return context.report({
          node: literal,
          messageId: 'templateLiteralLastLineIndent',
          fix(fixer) {
            return fixer.replaceTextRange(
              [literal.range[1] - lastLine.length - 1, literal.range[1]],
              doIndent('`', parentIndent),
            );
          },
        });
      }

      // remove the empty lines
      lines.pop();
      lines.shift();

      // +2 because we expect the string contents are indented one level
      const expectedIndent = parentIndent + 2;

      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      const firstLineIndent = START_OF_LINE_WHITESPACE_MATCHER.exec(
        lines[0],
      )![1];
      const requiresIndent = firstLineIndent.length > 0;
      if (requiresIndent) {
        if (firstLineIndent.length !== expectedIndent) {
          return context.report({
            node: literal,
            messageId: 'templateStringRequiresIndent',
            data: {
              indent: expectedIndent,
            },
          });
        }

        // quick-and-dirty validation that lines are roughly indented correctly
        for (const line of lines) {
          if (line.length === 0) {
            // empty lines are valid
            continue;
          }

          // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
          const matches = START_OF_LINE_WHITESPACE_MATCHER.exec(line)!;

          const indent = matches[1];
          if (indent.length < expectedIndent) {
            return context.report({
              node: literal,
              messageId: 'templateStringMinimumIndent',
              data: {
                indent: expectedIndent,
              },
            });
          }
        }

        // trim the lines to remove expectedIndent characters from the start
        // this makes it easier to check formatting
        for (let i = 0; i < lines.length; i += 1) {
          lines[i] = lines[i].substring(expectedIndent);
        }
      }

      const code = lines.join('\n');

      if (isNoFormatTagged) {
        if (literal.parent.type === AST_NODE_TYPES.TaggedTemplateExpression) {
          checkForUnnecesaryNoFormat(code, literal.parent);
        }
        return;
      }

      const formatted = getCodeFormattedOrReport(code, literal);
      if (formatted && formatted !== code) {
        const formattedIndented = requiresIndent
          ? formatted
              .split('\n')
              .map(l => doIndent(l, expectedIndent))
              .join('\n')
          : formatted;

        return context.report({
          node: literal,
          messageId: isErrorTest
            ? 'invalidFormattingErrorTest'
            : 'invalidFormatting',
          fix(fixer) {
            return fixer.replaceText(
              literal,
              `\`\n${escapeTemplateString(formattedIndented)}\n${doIndent(
                '',
                parentIndent,
              )}\``,
            );
          },
        });
      }
    }
```
</details>

- **Parameters**:
  - `literal: TSESTree.TemplateLiteral`
  - `isErrorTest: boolean`
  - `isNoFormatTagged: boolean`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getQuote`
  - `fixer.replaceTextRange`
  - `text.split`
  - `lines[0].trimEnd`
  - `lastLine.trimStart`
  - `getExpectedIndentForNode`
  - `doIndent`
  - `lines.pop`
  - `lines.shift`
  - `START_OF_LINE_WHITESPACE_MATCHER.exec`
  - `lines[i].substring`
  - `lines.join`
  - `checkForUnnecesaryNoFormat`
  - `getCodeFormattedOrReport`
  - `formatted
              .split('\n')
              .map(l => doIndent(l, expectedIndent))
              .join`
  - `fixer.replaceText`
  - `escapeTemplateString`
- **Internal Comments**:
```
// ignore template literals with ${expressions} for simplicity
// don't use template strings for single line tests
// prettier will trim out the end of line on save, but eslint will check before then (x2)
// last line can be indented (x2)
// multiline template strings must have an empty first/last line
// remove the empty lines (x4)
// +2 because we expect the string contents are indented one level (x2)
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x4)
// quick-and-dirty validation that lines are roughly indented correctly
// empty lines are valid
// trim the lines to remove expectedIndent characters from the start
// this makes it easier to check formatting
```

### `isNoFormatTemplateTag(tag: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isNoFormatTemplateTag(tag: TSESTree.Expression): boolean {
      return tag.type === AST_NODE_TYPES.Identifier && tag.name === 'noFormat';
    }
```
</details>

- **Parameters**:
  - `tag: TSESTree.Expression`
- **Return Type**: `boolean`
### `checkForUnnecesaryNoFormat(text: string, expr: TSESTree.TaggedTemplateExpression): void`

<details><summary>Code</summary>

```ts
function checkForUnnecesaryNoFormat(
      text: string,
      expr: TSESTree.TaggedTemplateExpression,
    ): void {
      const formatted = getCodeFormatted(text);
      if (formatted === text) {
        context.report({
          node: expr,
          messageId: 'noUnnecessaryNoFormat',
          fix(fixer) {
            if (expr.loc.start.line === expr.loc.end.line) {
              return fixer.replaceText(expr, `'${escapeTemplateString(text)}'`);
            }
            return fixer.replaceText(expr.tag, '');
          },
        });
      }
    }
```
</details>

- **Parameters**:
  - `text: string`
  - `expr: TSESTree.TaggedTemplateExpression`
- **Return Type**: `void`
- **Calls**:
  - `getCodeFormatted`
  - `context.report`
  - `fixer.replaceText`
  - `escapeTemplateString`
### `checkTaggedTemplateExpression(expr: TSESTree.TaggedTemplateExpression, isErrorTest: boolean): void`

<details><summary>Code</summary>

```ts
function checkTaggedTemplateExpression(
      expr: TSESTree.TaggedTemplateExpression,
      isErrorTest: boolean,
    ): void {
      if (isNoFormatTemplateTag(expr.tag)) {
        const { cooked } = expr.quasi.quasis[0].value;
        checkForUnnecesaryNoFormat(cooked, expr);
      } else {
        return;
      }

      if (expr.loc.start.line === expr.loc.end.line) {
        // all we do on single line test cases is check format, but there's no formatting to do
        return;
      }

      checkTemplateLiteral(
        expr.quasi,
        isErrorTest,
        isNoFormatTemplateTag(expr.tag),
      );
    }
```
</details>

- **Parameters**:
  - `expr: TSESTree.TaggedTemplateExpression`
  - `isErrorTest: boolean`
- **Return Type**: `void`
- **Calls**:
  - `isNoFormatTemplateTag`
  - `checkForUnnecesaryNoFormat`
  - `checkTemplateLiteral`
- **Internal Comments**:
```
// all we do on single line test cases is check format, but there's no formatting to do
```

### `checkCallExpression(callExpr: TSESTree.CallExpression, isErrorTest: boolean): void`

<details><summary>Code</summary>

```ts
function checkCallExpression(
      callExpr: TSESTree.CallExpression,
      isErrorTest: boolean,
    ): void {
      if (callExpr.callee.type !== AST_NODE_TYPES.MemberExpression) {
        return;
      }
      const memberExpr = callExpr.callee;
      // handle cases like 'aa'.trimRight and `aa`.trimRight()
      checkExpression(memberExpr.object, isErrorTest);
    }
```
</details>

- **Parameters**:
  - `callExpr: TSESTree.CallExpression`
  - `isErrorTest: boolean`
- **Return Type**: `void`
- **Calls**:
  - `checkExpression`
- **Internal Comments**:
```
// handle cases like 'aa'.trimRight and `aa`.trimRight() (x3)
```

### `checkInvalidTest(test: TSESTree.ObjectExpression, isErrorTest: boolean): void`

<details><summary>Code</summary>

```ts
function checkInvalidTest(
      test: TSESTree.ObjectExpression,
      isErrorTest = true,
    ): void {
      if (checkedObjects.has(test)) {
        return;
      }

      checkedObjects.add(test);

      for (const prop of test.properties) {
        if (
          prop.type !== AST_NODE_TYPES.Property ||
          prop.computed ||
          prop.key.type !== AST_NODE_TYPES.Identifier
        ) {
          continue;
        }

        if (prop.key.name === 'code') {
          checkExpression(prop.value, isErrorTest);
        }
      }
    }
```
</details>

- **Parameters**:
  - `test: TSESTree.ObjectExpression`
  - `isErrorTest: boolean`
- **Return Type**: `void`
- **Calls**:
  - `checkedObjects.has`
  - `checkedObjects.add`
  - `checkExpression`
### `checkValidTest(tests: TSESTree.ArrayExpression): void`

<details><summary>Code</summary>

```ts
function checkValidTest(tests: TSESTree.ArrayExpression): void {
      for (const test of tests.elements) {
        switch (test?.type) {
          case AST_NODE_TYPES.ObjectExpression:
            // delegate object-style tests to the invalid checker
            checkInvalidTest(test, false);
            break;

          default:
            checkExpression(test, false);
            break;
        }
      }
    }
```
</details>

- **Parameters**:
  - `tests: TSESTree.ArrayExpression`
- **Return Type**: `void`
- **Calls**:
  - `checkInvalidTest`
  - `checkExpression`
- **Internal Comments**:
```
// delegate object-style tests to the invalid checker (x3)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    // This option exists so that rules like type-annotation-spacing can exist without every test needing a prettier-ignore
    formatWithPrettier?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'invalidFormatting'
  | 'invalidFormattingErrorTest'
  | 'noUnnecessaryNoFormat'
  | 'prettierException'
  | 'singleLineQuotes'
  | 'templateLiteralEmptyEnds'
  | 'templateLiteralLastLineIndent'
  | 'templateStringMinimumIndent'
  | 'templateStringRequiresIndent';
```

### `FormattingError`

```ts
type FormattingError = {
  codeFrame: string;
  loc?: unknown;
} & Error;
```


---