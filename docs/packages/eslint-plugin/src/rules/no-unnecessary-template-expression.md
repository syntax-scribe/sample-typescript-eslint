[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-template-expression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 20 |
| 🧱 Classes | 0 |
| 📦 Imports | 13 |
| 📊 Variables & Constants | 8 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-template-expression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstraintInfo` | `../util` |
| `getMovedNodeCode` | `../util` |
| `getParserServices` | `../util` |
| `isNodeOfType` | `../util` |
| `isTypeFlagSet` | `../util` |
| `isUndefinedIdentifier` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `rangeToLoc` | `../util/rangeToLoc` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `evenNumOfBackslashesRegExp` | `RegExp` | const | `/(?<!(?:[^\\]|^)(?:\\\\)*\\)/` | ✗ |
| `maybeLiteral` | `any` | const | `node.type === AST_NODE_TYPES.TSLiteralType ? node.literal : node` | ✗ |
| `maybeTemplateLiteral` | `any` | const | `node.type === AST_NODE_TYPES.TSLiteralType ? node.literal : node` | ✗ |
| `nextCharacterIsOpeningCurlyBrace` | `boolean` | let/var | `false` | ✗ |
| `reportDescriptors` | `TSESLint.ReportDescriptor<MessageId>[]` | const | `[]` | ✗ |
| `fixers` | `((fixer: TSESLint.RuleFixer) => TSESLint.RuleFix[])[]` | const | `[]` | ✗ |
| `warnLocStart` | `number` | const | `prevQuasi.range[1] - 2` | ✗ |
| `warnLocEnd` | `any` | const | `nextQuasi.range[0] + 1` | ✗ |


---

## Functions

### `endsWithUnescapedDollarSign(str: string): boolean`

<details><summary>Code</summary>

```ts
function endsWithUnescapedDollarSign(str: string): boolean {
  return new RegExp(`${evenNumOfBackslashesRegExp.source}\\$$`).test(str);
}
```
</details>

- **Parameters**:
  - `str: string`
- **Return Type**: `boolean`
- **Calls**:
  - `new RegExp(`${evenNumOfBackslashesRegExp.source}\\$$`).test`
### `isStringLike(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isStringLike(type: ts.Type): boolean {
      return isTypeFlagSet(type, ts.TypeFlags.StringLike);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ../util)`
### `isUnderlyingTypeString(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isUnderlyingTypeString(type: ts.Type): boolean {
      if (type.isUnion()) {
        return type.types.every(isStringLike);
      }

      if (type.isIntersection()) {
        return type.types.some(isStringLike);
      }

      return isStringLike(type);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isUnion`
  - `type.types.every`
  - `type.isIntersection`
  - `type.types.some`
  - `isStringLike`
### `isEnumMemberType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isEnumMemberType(type: ts.Type): boolean {
      return tsutils.typeConstituents(type).some(t => {
        const symbol = t.getSymbol();
        return !!(
          symbol?.valueDeclaration && ts.isEnumMember(symbol.valueDeclaration)
        );
      });
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.typeConstituents(type).some`
  - `t.getSymbol`
  - `ts.isEnumMember`
### `isTemplateLiteral(node: TSESTree.Node): node is TSESTree.TemplateLiteral`

<details><summary>Code</summary>

```ts
function isTemplateLiteral(
      node: TSESTree.Node,
    ): node is TSESTree.TemplateLiteral {
      return node.type === AST_NODE_TYPES.TemplateLiteral;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.TemplateLiteral`
### `isInfinityIdentifier(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isInfinityIdentifier(node: TSESTree.Node): boolean {
      return (
        node.type === AST_NODE_TYPES.Identifier && node.name === 'Infinity'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isNaNIdentifier(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isNaNIdentifier(node: TSESTree.Node): boolean {
      return node.type === AST_NODE_TYPES.Identifier && node.name === 'NaN';
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `isFixableIdentifier(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isFixableIdentifier(node: TSESTree.Node): boolean {
      return (
        isUndefinedIdentifier(node) ||
        isInfinityIdentifier(node) ||
        isNaNIdentifier(node)
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `isUndefinedIdentifier (from ../util)`
  - `isInfinityIdentifier`
  - `isNaNIdentifier`
### `hasCommentsBetweenQuasi(startQuasi: TSESTree.TemplateElement, endQuasi: TSESTree.TemplateElement): boolean`

<details><summary>Code</summary>

```ts
function hasCommentsBetweenQuasi(
      startQuasi: TSESTree.TemplateElement,
      endQuasi: TSESTree.TemplateElement,
    ): boolean {
      const startToken = nullThrows(
        context.sourceCode.getTokenByRangeStart(startQuasi.range[0]),
        NullThrowsReasons.MissingToken('`${', 'opening template literal'),
      );
      const endToken = nullThrows(
        context.sourceCode.getTokenByRangeStart(endQuasi.range[0]),
        NullThrowsReasons.MissingToken('}', 'closing template literal'),
      );

      return context.sourceCode.commentsExistBetween(startToken, endToken);
    }
```
</details>

- **Parameters**:
  - `startQuasi: TSESTree.TemplateElement`
  - `endQuasi: TSESTree.TemplateElement`
- **Return Type**: `boolean`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenByRangeStart`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.commentsExistBetween`
### `isTrivialInterpolation(node: TSESTree.TemplateLiteral | TSESTree.TSTemplateLiteralType): boolean`

<details><summary>Code</summary>

```ts
function isTrivialInterpolation(
      node: TSESTree.TemplateLiteral | TSESTree.TSTemplateLiteralType,
    ) {
      return (
        node.quasis.length === 2 &&
        node.quasis[0].value.raw === '' &&
        node.quasis[1].value.raw === ''
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TemplateLiteral | TSESTree.TSTemplateLiteralType`
- **Return Type**: `boolean`
### `getInterpolations(node: TemplateLiteralTypeOrValue): TSESTree.Expression[] | TSESTree.TypeNode[]`

<details><summary>Code</summary>

```ts
function getInterpolations(
      node: TemplateLiteralTypeOrValue,
    ): TSESTree.Expression[] | TSESTree.TypeNode[] {
      if (node.type === AST_NODE_TYPES.TemplateLiteral) {
        return node.expressions;
      }
      return node.types;
    }
```
</details>

- **Parameters**:
  - `node: TemplateLiteralTypeOrValue`
- **Return Type**: `TSESTree.Expression[] | TSESTree.TypeNode[]`
### `getInterpolationInfos(node: TemplateLiteralTypeOrValue): InterpolationInfo[]`

<details><summary>Code</summary>

```ts
function getInterpolationInfos(
      node: TemplateLiteralTypeOrValue,
    ): InterpolationInfo[] {
      return getInterpolations(node).map((interpolation, index) => ({
        interpolation,
        nextQuasi: node.quasis[index + 1],
        prevQuasi: node.quasis[index],
      }));
    }
```
</details>

- **Parameters**:
  - `node: TemplateLiteralTypeOrValue`
- **Return Type**: `InterpolationInfo[]`
- **Calls**:
  - `getInterpolations(node).map`
### `getLiteral(node: TSESTree.Expression | TSESTree.TypeNode): TSESTree.Literal | null`

<details><summary>Code</summary>

```ts
function getLiteral(
      node: TSESTree.Expression | TSESTree.TypeNode,
    ): TSESTree.Literal | null {
      const maybeLiteral =
        node.type === AST_NODE_TYPES.TSLiteralType ? node.literal : node;
      return isLiteral(maybeLiteral) ? maybeLiteral : null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression | TSESTree.TypeNode`
- **Return Type**: `TSESTree.Literal | null`
- **Calls**:
  - `isLiteral`
### `getTemplateLiteral(node: TSESTree.Expression | TSESTree.TypeNode): TSESTree.TemplateLiteral | null`

<details><summary>Code</summary>

```ts
function getTemplateLiteral(
      node: TSESTree.Expression | TSESTree.TypeNode,
    ): TSESTree.TemplateLiteral | null {
      const maybeTemplateLiteral =
        node.type === AST_NODE_TYPES.TSLiteralType ? node.literal : node;
      return isTemplateLiteral(maybeTemplateLiteral)
        ? maybeTemplateLiteral
        : null;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression | TSESTree.TypeNode`
- **Return Type**: `TSESTree.TemplateLiteral | null`
- **Calls**:
  - `isTemplateLiteral`
### `reportSingleInterpolation(node: TemplateLiteralTypeOrValue): void`

<details><summary>Code</summary>

```ts
function reportSingleInterpolation(node: TemplateLiteralTypeOrValue): void {
      const interpolations = getInterpolations(node);
      context.report({
        loc: rangeToLoc(context.sourceCode, [
          interpolations[0].range[0] - 2,
          interpolations[0].range[1] + 1,
        ]),
        messageId: 'noUnnecessaryTemplateExpression',
        fix(fixer): TSESLint.RuleFix | null {
          const wrappingCode = getMovedNodeCode({
            destinationNode: node,
            nodeToMove: interpolations[0],
            sourceCode: context.sourceCode,
          });

          return fixer.replaceText(node, wrappingCode);
        },
      });
    }
```
</details>

- **Parameters**:
  - `node: TemplateLiteralTypeOrValue`
- **Return Type**: `void`
- **Calls**:
  - `getInterpolations`
  - `context.report`
  - `rangeToLoc (from ../util/rangeToLoc)`
  - `getMovedNodeCode (from ../util)`
  - `fixer.replaceText`
### `isUnncessaryValueInterpolation({
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo): boolean`

<details><summary>Code</summary>

```ts
function isUnncessaryValueInterpolation({
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo): boolean {
      if (hasCommentsBetweenQuasi(prevQuasi, nextQuasi)) {
        return false;
      }

      if (isFixableIdentifier(interpolation)) {
        return true;
      }

      if (isLiteral(interpolation)) {
        // allow trailing whitespace literal
        if (startsWithNewLine(nextQuasi.value.raw)) {
          return !(
            typeof interpolation.value === 'string' &&
            isWhitespace(interpolation.value)
          );
        }
        return true;
      }

      if (isTemplateLiteral(interpolation)) {
        // allow trailing whitespace literal
        if (startsWithNewLine(nextQuasi.value.raw)) {
          return !(
            interpolation.quasis.length === 1 &&
            isWhitespace(interpolation.quasis[0].value.raw)
          );
        }
        return true;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `{
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo`
- **Return Type**: `boolean`
- **Calls**:
  - `hasCommentsBetweenQuasi`
  - `isFixableIdentifier`
  - `isLiteral`
  - `startsWithNewLine`
  - `isWhitespace`
  - `isTemplateLiteral`
- **Internal Comments**:
```
// allow trailing whitespace literal (x2)
```

### `isUnncessaryTypeInterpolation({
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo): boolean`

<details><summary>Code</summary>

```ts
function isUnncessaryTypeInterpolation({
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo): boolean {
      if (hasCommentsBetweenQuasi(prevQuasi, nextQuasi)) {
        return false;
      }

      const literal = getLiteral(interpolation);
      if (literal) {
        // allow trailing whitespace literal
        if (startsWithNewLine(nextQuasi.value.raw)) {
          return !(
            typeof literal.value === 'string' && isWhitespace(literal.value)
          );
        }
        return true;
      }

      if (
        interpolation.type === AST_NODE_TYPES.TSNullKeyword ||
        interpolation.type === AST_NODE_TYPES.TSUndefinedKeyword
      ) {
        return true;
      }

      const templateLiteral = getTemplateLiteral(interpolation);
      if (templateLiteral) {
        // allow trailing whitespace literal
        if (startsWithNewLine(nextQuasi.value.raw)) {
          return !(
            templateLiteral.quasis.length === 1 &&
            isWhitespace(templateLiteral.quasis[0].value.raw)
          );
        }
        return true;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `{
      interpolation,
      nextQuasi,
      prevQuasi,
    }: InterpolationInfo`
- **Return Type**: `boolean`
- **Calls**:
  - `hasCommentsBetweenQuasi`
  - `getLiteral`
  - `startsWithNewLine`
  - `isWhitespace`
  - `getTemplateLiteral`
- **Internal Comments**:
```
// allow trailing whitespace literal (x2)
```

### `getReportDescriptors(infos: InterpolationInfo[]): TSESLint.ReportDescriptor<MessageId>[]`

<details><summary>Code</summary>

```ts
function getReportDescriptors(
      infos: InterpolationInfo[],
    ): TSESLint.ReportDescriptor<MessageId>[] {
      let nextCharacterIsOpeningCurlyBrace = false;
      const reportDescriptors: TSESLint.ReportDescriptor<MessageId>[] = [];
      const reversedInfos = [...infos].reverse();
      for (const { interpolation, nextQuasi, prevQuasi } of reversedInfos) {
        const fixers: ((fixer: TSESLint.RuleFixer) => TSESLint.RuleFix[])[] =
          [];

        if (nextQuasi.value.raw !== '') {
          nextCharacterIsOpeningCurlyBrace =
            nextQuasi.value.raw.startsWith('{');
        }

        const literal = getLiteral(interpolation);
        const templateLiteral = getTemplateLiteral(interpolation);
        if (literal) {
          let escapedValue = (
            typeof literal.value === 'string'
              ? // The value is already a string, so we're removing quotes:
                // "'va`lue'" -> "va`lue"
                literal.raw.slice(1, -1)
              : // The value may be one of number | bigint | boolean | RegExp | null.
                // In regular expressions, we escape every backslash
                String(literal.value).replaceAll('\\', '\\\\')
          )
            // The string or RegExp may contain ` or ${.
            // We want both of these to be escaped in the final template expression.
            //
            // A pair of backslashes means "escaped backslash", so backslashes
            // from this pair won't escape ` or ${. Therefore, to escape these
            // sequences in the resulting template expression, we need to escape
            // all sequences that are preceded by an even number of backslashes.
            //
            // This RegExp does the following transformations:
            // \` -> \`
            // \\` -> \\\`
            // \${ -> \${
            // \\${ -> \\\${
            .replaceAll(
              new RegExp(`${evenNumOfBackslashesRegExp.source}(\`|\\\${)`, 'g'),
              '\\$1',
            );

          // `...${'...$'}{...`
          //           ^^^^
          if (
            nextCharacterIsOpeningCurlyBrace &&
            endsWithUnescapedDollarSign(escapedValue)
          ) {
            escapedValue = escapedValue.replaceAll(/\$$/g, '\\$');
          }

          if (escapedValue.length !== 0) {
            nextCharacterIsOpeningCurlyBrace = escapedValue.startsWith('{');
          }

          fixers.push(fixer => [fixer.replaceText(literal, escapedValue)]);
        } else if (templateLiteral) {
          // Since we iterate from the last expression to the first,
          // a subsequent expression can tell the current expression
          // that it starts with {.
          //
          // `... ${`... $`}${'{...'} ...`
          //             ^     ^ subsequent expression starts with {
          //             current expression ends with a dollar sign,
          //             so '$' + '{' === '${' (bad news for us).
          //             Let's escape the dollar sign at the end.
          if (
            nextCharacterIsOpeningCurlyBrace &&
            endsWithUnescapedDollarSign(
              templateLiteral.quasis[templateLiteral.quasis.length - 1].value
                .raw,
            )
          ) {
            fixers.push(fixer => [
              fixer.replaceTextRange(
                [templateLiteral.range[1] - 2, templateLiteral.range[1] - 2],
                '\\',
              ),
            ]);
          }
          if (
            templateLiteral.quasis.length === 1 &&
            templateLiteral.quasis[0].value.raw.length !== 0
          ) {
            nextCharacterIsOpeningCurlyBrace =
              templateLiteral.quasis[0].value.raw.startsWith('{');
          }

          // Remove the beginning and trailing backtick characters.
          fixers.push(fixer => [
            fixer.removeRange([
              templateLiteral.range[0],
              templateLiteral.range[0] + 1,
            ]),
            fixer.removeRange([
              templateLiteral.range[1] - 1,
              templateLiteral.range[1],
            ]),
          ]);
        } else {
          nextCharacterIsOpeningCurlyBrace = false;
        }

        // `... $${'{...'} ...`
        //      ^^^^^
        if (
          nextCharacterIsOpeningCurlyBrace &&
          endsWithUnescapedDollarSign(prevQuasi.value.raw)
        ) {
          fixers.push(fixer => [
            fixer.replaceTextRange(
              [prevQuasi.range[1] - 3, prevQuasi.range[1] - 2],
              '\\$',
            ),
          ]);
        }

        const warnLocStart = prevQuasi.range[1] - 2;
        const warnLocEnd = nextQuasi.range[0] + 1;
        reportDescriptors.push({
          loc: rangeToLoc(context.sourceCode, [warnLocStart, warnLocEnd]),
          messageId: 'noUnnecessaryTemplateExpression',
          fix(fixer): TSESLint.RuleFix[] {
            return [
              // Remove the quasis' parts that are related to the current expression.
              fixer.removeRange([warnLocStart, interpolation.range[0]]),
              fixer.removeRange([interpolation.range[1], warnLocEnd]),

              ...fixers.flatMap(cb => cb(fixer)),
            ];
          },
        });
      }
      return reportDescriptors;
    }
```
</details>

- **Parameters**:
  - `infos: InterpolationInfo[]`
- **Return Type**: `TSESLint.ReportDescriptor<MessageId>[]`
- **Calls**:
  - `[...infos].reverse`
  - `nextQuasi.value.raw.startsWith`
  - `getLiteral`
  - `getTemplateLiteral`
  - `(
            typeof literal.value === 'string'
              ? // The value is already a string, so we're removing quotes:
                // "'va`lue'" -> "va`lue"
                literal.raw.slice(1, -1)
              : // The value may be one of number | bigint | boolean | RegExp | null.
                // In regular expressions, we escape every backslash
                String(literal.value).replaceAll('\\', '\\\\')
          )
            // The string or RegExp may contain ` or ${.
            // We want both of these to be escaped in the final template expression.
            //
            // A pair of backslashes means "escaped backslash", so backslashes
            // from this pair won't escape ` or ${. Therefore, to escape these
            // sequences in the resulting template expression, we need to escape
            // all sequences that are preceded by an even number of backslashes.
            //
            // This RegExp does the following transformations:
            // \` -> \`
            // \\` -> \\\`
            // \${ -> \${
            // \\${ -> \\\${
            .replaceAll`
  - `literal.raw.slice`
  - `String(literal.value).replaceAll`
  - `endsWithUnescapedDollarSign`
  - `escapedValue.replaceAll`
  - `escapedValue.startsWith`
  - `fixers.push`
  - `fixer.replaceText`
  - `fixer.replaceTextRange`
  - `templateLiteral.quasis[0].value.raw.startsWith`
  - `fixer.removeRange`
  - `reportDescriptors.push`
  - `rangeToLoc (from ../util/rangeToLoc)`
  - `fixers.flatMap`
  - `cb`
- **Internal Comments**:
```
// "'va`lue'" -> "va`lue" (x4)
// In regular expressions, we escape every backslash (x4)
// `...${'...$'}{...`
//           ^^^^
// Since we iterate from the last expression to the first,
// a subsequent expression can tell the current expression
// that it starts with {.
//
// `... ${`... $`}${'{...'} ...`
//             ^     ^ subsequent expression starts with {
//             current expression ends with a dollar sign,
//             so '$' + '{' === '${' (bad news for us).
//             Let's escape the dollar sign at the end.
// Remove the beginning and trailing backtick characters. (x4)
// `... $${'{...'} ...`
//      ^^^^^
// Remove the quasis' parts that are related to the current expression. (x3)
```

### `isWhitespace(x: string): boolean`

<details><summary>Code</summary>

```ts
function isWhitespace(x: string): boolean {
  // allow empty string too since we went to allow
  // `      ${''}
  // `;
  //
  // in addition to
  // `${'        '}
  // `;
  //
  return /^\s*$/.test(x);
}
```
</details>

- **Parameters**:
  - `x: string`
- **Return Type**: `boolean`
- **Calls**:
  - `/^\s*$/.test`
- **Internal Comments**:
```
// allow empty string too since we went to allow
// `      ${''}
// `; (x2)
// (x2)
// in addition to
// `${'        '}
```

### `startsWithNewLine(x: string): boolean`

<details><summary>Code</summary>

```ts
function startsWithNewLine(x: string): boolean {
  return x.startsWith('\n') || x.startsWith('\r\n');
}
```
</details>

- **Parameters**:
  - `x: string`
- **Return Type**: `boolean`
- **Calls**:
  - `x.startsWith`

---

## Interfaces

### `InterpolationInfo`

<details><summary>Interface Code</summary>

```ts
interface InterpolationInfo {
  interpolation: TSESTree.Expression | TSESTree.TypeNode;
  prevQuasi: TSESTree.TemplateElement;
  nextQuasi: TSESTree.TemplateElement;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `interpolation` | `TSESTree.Expression | TSESTree.TypeNode` | ✗ |  |
| `prevQuasi` | `TSESTree.TemplateElement` | ✗ |  |
| `nextQuasi` | `TSESTree.TemplateElement` | ✗ |  |


---

## Type Aliases

### `MessageId`

```ts
type MessageId = 'noUnnecessaryTemplateExpression';
```

### `TemplateLiteralTypeOrValue`

```ts
type TemplateLiteralTypeOrValue = | TSESTree.TemplateLiteral
  | TSESTree.TSTemplateLiteralType;
```


---