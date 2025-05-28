[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-imports.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 10 |
| 🧱 Classes | 0 |
| 📦 Imports | 14 |
| 📊 Variables & Constants | 30 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 4 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-type-imports.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleListener` | `@typescript-eslint/utils/eslint-utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `formatWordList` | `../util` |
| `getParserServices` | `../util` |
| `isClosingBraceToken` | `../util` |
| `isCommaToken` | `../util` |
| `isImportKeyword` | `../util` |
| `isOpeningBraceToken` | `../util` |
| `isTypeKeyword` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `prefer` | `any` | const | `option.prefer ?? 'type-imports'` | ✗ |
| `disallowTypeAnnotations` | `boolean` | const | `option.disallowTypeAnnotations !== false` | ✗ |
| `selectors` | `RuleListener` | const | `{}` | ✗ |
| `fixStyle` | `any` | const | `option.fixStyle ?? 'separate-type-imports'` | ✗ |
| `hasDecoratorMetadata` | `boolean` | let/var | `false` | ✗ |
| `sourceImportsMap` | `Record<string, SourceImports>` | const | `{}` | ✗ |
| `emitDecoratorMetadata` | `any` | const | `getParserServices(context, true).emitDecoratorMetadata ?? false` | ✗ |
| `experimentalDecorators` | `any` | const | `getParserServices(context, true).experimentalDecorators ?? false` | ✗ |
| `source` | `any` | const | `node.source.value` | ✗ |
| `sourceImports` | `SourceImports` | const | `sourceImportsMap[source]` | ✗ |
| `typeSpecifiers` | `TSESTree.ImportClause[]` | const | `[]` | ✗ |
| `inlineTypeSpecifiers` | `TSESTree.ImportSpecifier[]` | const | `[]` | ✗ |
| `valueSpecifiers` | `TSESTree.ImportClause[]` | const | `[]` | ✗ |
| `unusedSpecifiers` | `TSESTree.ImportClause[]` | const | `[]` | ✗ |
| `parent` | `any` | let/var | `ref.identifier.parent as TSESTree.Node | undefined` | ✗ |
| `child` | `TSESTree.Node` | let/var | `ref.identifier` | ✗ |
| `defaultSpecifier` | `any` | const | `node.specifiers[0].type === AST_NODE_TYPES.ImportDefaultSpecifier
          ? node.specifiers[0]
          : null` | ✗ |
| `namespaceSpecifier` | `any` | const | `node.specifiers.find(
          (specifier): specifier is TSESTree.ImportNamespaceSpecifier =>
            specifier.type === AST_NODE_TYPES.ImportNamespaceSpecifier,
        ) ?? null` | ✗ |
| `typeNamedSpecifiersTexts` | `string[]` | const | `[]` | ✗ |
| `removeTypeNamedSpecifiers` | `TSESLint.RuleFix[]` | const | `[]` | ✗ |
| `namedSpecifierGroups` | `TSESTree.ImportSpecifier[][]` | const | `[]` | ✗ |
| `group` | `TSESTree.ImportSpecifier[]` | let/var | `[]` | ✗ |
| `first` | `TSESTree.ImportSpecifier` | const | `namedSpecifierGroup[0]` | ✗ |
| `last` | `TSESTree.ImportSpecifier` | const | `namedSpecifierGroup[namedSpecifierGroup.length - 1]` | ✗ |
| `removeRange` | `TSESTree.Range` | const | `[first.range[0], last.range[1]]` | ✗ |
| `textRange` | `TSESTree.Range` | const | `[...removeRange]` | ✗ |
| `isFirst` | `boolean` | const | `allNamedSpecifiers[0] === first` | ✗ |
| `isLast` | `boolean` | const | `allNamedSpecifiers[allNamedSpecifiers.length - 1] === last` | ✗ |
| `afterFixes` | `TSESLint.RuleFix[]` | let/var | `[]` | ✗ |
| `fixesRemoveTypeNamespaceSpecifier` | `TSESLint.RuleFix[]` | let/var | `[]` | ✗ |


---

## Functions

### `classifySpecifier(node: TSESTree.ImportDeclaration): {
      defaultSpecifier: TSESTree.ImportDefaultSpecifier | null;
      namedSpecifiers: TSESTree.ImportSpecifier[];
      namespaceSpecifier: TSESTree.ImportNamespaceSpecifier | null;
    }`

<details><summary>Code</summary>

```ts
function classifySpecifier(node: TSESTree.ImportDeclaration): {
      defaultSpecifier: TSESTree.ImportDefaultSpecifier | null;
      namedSpecifiers: TSESTree.ImportSpecifier[];
      namespaceSpecifier: TSESTree.ImportNamespaceSpecifier | null;
    } {
      const defaultSpecifier =
        node.specifiers[0].type === AST_NODE_TYPES.ImportDefaultSpecifier
          ? node.specifiers[0]
          : null;
      const namespaceSpecifier =
        node.specifiers.find(
          (specifier): specifier is TSESTree.ImportNamespaceSpecifier =>
            specifier.type === AST_NODE_TYPES.ImportNamespaceSpecifier,
        ) ?? null;
      const namedSpecifiers = node.specifiers.filter(
        (specifier): specifier is TSESTree.ImportSpecifier =>
          specifier.type === AST_NODE_TYPES.ImportSpecifier,
      );
      return {
        defaultSpecifier,
        namedSpecifiers,
        namespaceSpecifier,
      };
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportDeclaration`
- **Return Type**: `{
      defaultSpecifier: TSESTree.ImportDefaultSpecifier | null;
      namedSpecifiers: TSESTree.ImportSpecifier[];
      namespaceSpecifier: TSESTree.ImportNamespaceSpecifier | null;
    }`
- **Calls**:
  - `node.specifiers.find`
  - `node.specifiers.filter`
### `getFixesNamedSpecifiers(fixer: TSESLint.RuleFixer, node: TSESTree.ImportDeclaration, subsetNamedSpecifiers: TSESTree.ImportSpecifier[], allNamedSpecifiers: TSESTree.ImportSpecifier[]): {
      removeTypeNamedSpecifiers: TSESLint.RuleFix[];
      typeNamedSpecifiersText: string;
    }`

<details><summary>Code</summary>

```ts
function getFixesNamedSpecifiers(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.ImportDeclaration,
      subsetNamedSpecifiers: TSESTree.ImportSpecifier[],
      allNamedSpecifiers: TSESTree.ImportSpecifier[],
    ): {
      removeTypeNamedSpecifiers: TSESLint.RuleFix[];
      typeNamedSpecifiersText: string;
    } {
      if (allNamedSpecifiers.length === 0) {
        return {
          removeTypeNamedSpecifiers: [],
          typeNamedSpecifiersText: '',
        };
      }
      const typeNamedSpecifiersTexts: string[] = [];
      const removeTypeNamedSpecifiers: TSESLint.RuleFix[] = [];
      if (subsetNamedSpecifiers.length === allNamedSpecifiers.length) {
        // import Foo, {Type1, Type2} from 'foo'
        // import DefType, {Type1, Type2} from 'foo'
        const openingBraceToken = nullThrows(
          context.sourceCode.getTokenBefore(
            subsetNamedSpecifiers[0],
            isOpeningBraceToken,
          ),
          NullThrowsReasons.MissingToken('{', node.type),
        );
        const commaToken = nullThrows(
          context.sourceCode.getTokenBefore(openingBraceToken, isCommaToken),
          NullThrowsReasons.MissingToken(',', node.type),
        );
        const closingBraceToken = nullThrows(
          context.sourceCode.getFirstTokenBetween(
            openingBraceToken,
            node.source,
            isClosingBraceToken,
          ),
          NullThrowsReasons.MissingToken('}', node.type),
        );

        // import DefType, {...} from 'foo'
        //               ^^^^^^^ remove
        removeTypeNamedSpecifiers.push(
          fixer.removeRange([commaToken.range[0], closingBraceToken.range[1]]),
        );

        typeNamedSpecifiersTexts.push(
          context.sourceCode.text.slice(
            openingBraceToken.range[1],
            closingBraceToken.range[0],
          ),
        );
      } else {
        const namedSpecifierGroups: TSESTree.ImportSpecifier[][] = [];
        let group: TSESTree.ImportSpecifier[] = [];
        for (const namedSpecifier of allNamedSpecifiers) {
          if (subsetNamedSpecifiers.includes(namedSpecifier)) {
            group.push(namedSpecifier);
          } else if (group.length) {
            namedSpecifierGroups.push(group);
            group = [];
          }
        }
        if (group.length) {
          namedSpecifierGroups.push(group);
        }
        for (const namedSpecifiers of namedSpecifierGroups) {
          const { removeRange, textRange } = getNamedSpecifierRanges(
            namedSpecifiers,
            allNamedSpecifiers,
          );
          removeTypeNamedSpecifiers.push(fixer.removeRange(removeRange));

          typeNamedSpecifiersTexts.push(
            context.sourceCode.text.slice(...textRange),
          );
        }
      }
      return {
        removeTypeNamedSpecifiers,
        typeNamedSpecifiersText: typeNamedSpecifiersTexts.join(','),
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns information for fixing named specifiers, type or value
     */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.ImportDeclaration`
  - `subsetNamedSpecifiers: TSESTree.ImportSpecifier[]`
  - `allNamedSpecifiers: TSESTree.ImportSpecifier[]`
- **Return Type**: `{
      removeTypeNamedSpecifiers: TSESLint.RuleFix[];
      typeNamedSpecifiersText: string;
    }`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getFirstTokenBetween`
  - `removeTypeNamedSpecifiers.push`
  - `fixer.removeRange`
  - `typeNamedSpecifiersTexts.push`
  - `context.sourceCode.text.slice`
  - `subsetNamedSpecifiers.includes`
  - `group.push`
  - `namedSpecifierGroups.push`
  - `getNamedSpecifierRanges`
  - `typeNamedSpecifiersTexts.join`
- **Internal Comments**:
```
// import Foo, {Type1, Type2} from 'foo' (x2)
// import DefType, {Type1, Type2} from 'foo' (x2)
// import DefType, {...} from 'foo' (x4)
//               ^^^^^^^ remove (x4)
```

### `getNamedSpecifierRanges(namedSpecifierGroup: TSESTree.ImportSpecifier[], allNamedSpecifiers: TSESTree.ImportSpecifier[]): {
      removeRange: TSESTree.Range;
      textRange: TSESTree.Range;
    }`

<details><summary>Code</summary>

```ts
function getNamedSpecifierRanges(
      namedSpecifierGroup: TSESTree.ImportSpecifier[],
      allNamedSpecifiers: TSESTree.ImportSpecifier[],
    ): {
      removeRange: TSESTree.Range;
      textRange: TSESTree.Range;
    } {
      const first = namedSpecifierGroup[0];
      const last = namedSpecifierGroup[namedSpecifierGroup.length - 1];
      const removeRange: TSESTree.Range = [first.range[0], last.range[1]];
      const textRange: TSESTree.Range = [...removeRange];
      const before = nullThrows(
        context.sourceCode.getTokenBefore(first),
        NullThrowsReasons.MissingToken('token', 'first specifier'),
      );
      textRange[0] = before.range[1];
      if (isCommaToken(before)) {
        removeRange[0] = before.range[0];
      } else {
        removeRange[0] = before.range[1];
      }

      const isFirst = allNamedSpecifiers[0] === first;
      const isLast = allNamedSpecifiers[allNamedSpecifiers.length - 1] === last;
      const after = nullThrows(
        context.sourceCode.getTokenAfter(last),
        NullThrowsReasons.MissingToken('token', 'last specifier'),
      );
      textRange[1] = after.range[0];
      if ((isFirst || isLast) && isCommaToken(after)) {
        removeRange[1] = after.range[1];
      }

      return {
        removeRange,
        textRange,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns ranges for fixing named specifier.
     */
```

- **Parameters**:
  - `namedSpecifierGroup: TSESTree.ImportSpecifier[]`
  - `allNamedSpecifiers: TSESTree.ImportSpecifier[]`
- **Return Type**: `{
      removeRange: TSESTree.Range;
      textRange: TSESTree.Range;
    }`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
  - `isCommaToken (from ../util)`
  - `context.sourceCode.getTokenAfter`
### `fixInsertNamedSpecifiersInNamedSpecifierList(fixer: TSESLint.RuleFixer, target: TSESTree.ImportDeclaration, insertText: string): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
function fixInsertNamedSpecifiersInNamedSpecifierList(
      fixer: TSESLint.RuleFixer,
      target: TSESTree.ImportDeclaration,
      insertText: string,
    ): TSESLint.RuleFix {
      const closingBraceToken = nullThrows(
        context.sourceCode.getFirstTokenBetween(
          nullThrows(
            context.sourceCode.getFirstToken(target),
            NullThrowsReasons.MissingToken('token before', 'import'),
          ),
          target.source,
          isClosingBraceToken,
        ),
        NullThrowsReasons.MissingToken('}', target.type),
      );
      const before = nullThrows(
        context.sourceCode.getTokenBefore(closingBraceToken),
        NullThrowsReasons.MissingToken('token before', 'closing brace'),
      );
      if (!isCommaToken(before) && !isOpeningBraceToken(before)) {
        insertText = `,${insertText}`;
      }
      return fixer.insertTextBefore(closingBraceToken, insertText);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * insert specifiers to named import node.
     * e.g.
     * import type { Already, Type1, Type2 } from 'foo'
     *                        ^^^^^^^^^^^^^ insert
     */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `target: TSESTree.ImportDeclaration`
  - `insertText: string`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstTokenBetween`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenBefore`
  - `isCommaToken (from ../util)`
  - `isOpeningBraceToken (from ../util)`
  - `fixer.insertTextBefore`
### `fixInsertTypeKeywordInNamedSpecifierList(fixer: TSESLint.RuleFixer, typeSpecifiers: TSESTree.ImportSpecifier[]): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixInsertTypeKeywordInNamedSpecifierList(
      fixer: TSESLint.RuleFixer,
      typeSpecifiers: TSESTree.ImportSpecifier[],
    ): IterableIterator<TSESLint.RuleFix> {
      for (const spec of typeSpecifiers) {
        const insertText = context.sourceCode.text.slice(...spec.range);
        yield fixer.replaceTextRange(spec.range, `type ${insertText}`);
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * insert type keyword to named import node.
     * e.g.
     * import ADefault, { Already, type Type1, type Type2 } from 'foo'
     *                             ^^^^ insert
     */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `typeSpecifiers: TSESTree.ImportSpecifier[]`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `context.sourceCode.text.slice`
  - `fixer.replaceTextRange`
### `fixInlineTypeImportDeclaration(fixer: TSESLint.RuleFixer, report: ReportValueImport, sourceImports: SourceImports): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixInlineTypeImportDeclaration(
      fixer: TSESLint.RuleFixer,
      report: ReportValueImport,
      sourceImports: SourceImports,
    ): IterableIterator<TSESLint.RuleFix> {
      const { node } = report;
      // For a value import, will only add an inline type to named specifiers
      const { namedSpecifiers } = classifySpecifier(node);
      const typeNamedSpecifiers = namedSpecifiers.filter(specifier =>
        report.typeSpecifiers.includes(specifier),
      );

      if (sourceImports.valueImport) {
        // add import named type specifiers to its value import
        // import ValueA, { type A }
        //                  ^^^^ insert
        const { namedSpecifiers: valueImportNamedSpecifiers } =
          classifySpecifier(sourceImports.valueImport);
        if (
          sourceImports.valueOnlyNamedImport ||
          valueImportNamedSpecifiers.length
        ) {
          yield* fixInsertTypeKeywordInNamedSpecifierList(
            fixer,
            typeNamedSpecifiers,
          );
        }
      }
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `report: ReportValueImport`
  - `sourceImports: SourceImports`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `classifySpecifier`
  - `namedSpecifiers.filter`
  - `report.typeSpecifiers.includes`
  - `fixInsertTypeKeywordInNamedSpecifierList`
- **Internal Comments**:
```
// For a value import, will only add an inline type to named specifiers (x2)
// add import named type specifiers to its value import (x2)
// import ValueA, { type A } (x2)
//                  ^^^^ insert (x2)
```

### `fixToTypeImportDeclaration(fixer: TSESLint.RuleFixer, report: ReportValueImport, sourceImports: SourceImports): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixToTypeImportDeclaration(
      fixer: TSESLint.RuleFixer,
      report: ReportValueImport,
      sourceImports: SourceImports,
    ): IterableIterator<TSESLint.RuleFix> {
      const { node } = report;

      const { defaultSpecifier, namedSpecifiers, namespaceSpecifier } =
        classifySpecifier(node);

      if (namespaceSpecifier && !defaultSpecifier) {
        // import * as types from 'foo'

        // checks for presence of import assertions
        if (node.attributes.length === 0) {
          yield* fixInsertTypeSpecifierForImportDeclaration(fixer, node, false);
        }
        return;
      }

      if (defaultSpecifier) {
        if (
          report.typeSpecifiers.includes(defaultSpecifier) &&
          namedSpecifiers.length === 0 &&
          !namespaceSpecifier
        ) {
          // import Type from 'foo'
          yield* fixInsertTypeSpecifierForImportDeclaration(fixer, node, true);
          return;
        }

        if (
          fixStyle === 'inline-type-imports' &&
          !report.typeSpecifiers.includes(defaultSpecifier) &&
          namedSpecifiers.length > 0 &&
          !namespaceSpecifier
        ) {
          // if there is a default specifier but it isn't a type specifier, then just add the inline type modifier to the named specifiers
          // import AValue, {BValue, Type1, Type2} from 'foo'
          yield* fixInlineTypeImportDeclaration(fixer, report, sourceImports);
          return;
        }
      } else if (!namespaceSpecifier) {
        if (
          fixStyle === 'inline-type-imports' &&
          namedSpecifiers.some(specifier =>
            report.typeSpecifiers.includes(specifier),
          )
        ) {
          // import {AValue, Type1, Type2} from 'foo'
          yield* fixInlineTypeImportDeclaration(fixer, report, sourceImports);
          return;
        }

        if (
          namedSpecifiers.every(specifier =>
            report.typeSpecifiers.includes(specifier),
          )
        ) {
          // import {Type1, Type2} from 'foo'
          yield* fixInsertTypeSpecifierForImportDeclaration(fixer, node, false);
          return;
        }
      }

      const typeNamedSpecifiers = namedSpecifiers.filter(specifier =>
        report.typeSpecifiers.includes(specifier),
      );

      const fixesNamedSpecifiers = getFixesNamedSpecifiers(
        fixer,
        node,
        typeNamedSpecifiers,
        namedSpecifiers,
      );
      const afterFixes: TSESLint.RuleFix[] = [];
      if (typeNamedSpecifiers.length) {
        if (sourceImports.typeOnlyNamedImport) {
          const insertTypeNamedSpecifiers =
            fixInsertNamedSpecifiersInNamedSpecifierList(
              fixer,
              sourceImports.typeOnlyNamedImport,
              fixesNamedSpecifiers.typeNamedSpecifiersText,
            );
          if (sourceImports.typeOnlyNamedImport.range[1] <= node.range[0]) {
            yield insertTypeNamedSpecifiers;
          } else {
            afterFixes.push(insertTypeNamedSpecifiers);
          }
        } else {
          // The import is both default and named.  Insert named on new line because can't mix default type import and named type imports
          // eslint-disable-next-line no-lonely-if
          if (fixStyle === 'inline-type-imports') {
            yield fixer.insertTextBefore(
              node,
              `import {${typeNamedSpecifiers
                .map(spec => {
                  const insertText = context.sourceCode.text.slice(
                    ...spec.range,
                  );
                  return `type ${insertText}`;
                })
                .join(
                  ', ',
                )}} from ${context.sourceCode.getText(node.source)};\n`,
            );
          } else {
            yield fixer.insertTextBefore(
              node,
              `import type {${
                fixesNamedSpecifiers.typeNamedSpecifiersText
              }} from ${context.sourceCode.getText(node.source)};\n`,
            );
          }
        }
      }

      const fixesRemoveTypeNamespaceSpecifier: TSESLint.RuleFix[] = [];
      if (
        namespaceSpecifier &&
        report.typeSpecifiers.includes(namespaceSpecifier)
      ) {
        // import Foo, * as Type from 'foo'
        // import DefType, * as Type from 'foo'
        // import DefType, * as Type from 'foo'
        const commaToken = nullThrows(
          context.sourceCode.getTokenBefore(namespaceSpecifier, isCommaToken),
          NullThrowsReasons.MissingToken(',', node.type),
        );

        // import Def, * as Ns from 'foo'
        //           ^^^^^^^^^ remove
        fixesRemoveTypeNamespaceSpecifier.push(
          fixer.removeRange([commaToken.range[0], namespaceSpecifier.range[1]]),
        );

        // import type * as Ns from 'foo'
        // ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ insert
        yield fixer.insertTextBefore(
          node,
          `import type ${context.sourceCode.getText(
            namespaceSpecifier,
          )} from ${context.sourceCode.getText(node.source)};\n`,
        );
      }
      if (
        defaultSpecifier &&
        report.typeSpecifiers.includes(defaultSpecifier)
      ) {
        if (report.typeSpecifiers.length === node.specifiers.length) {
          const importToken = nullThrows(
            context.sourceCode.getFirstToken(node, isImportKeyword),
            NullThrowsReasons.MissingToken('import', node.type),
          );
          // import type Type from 'foo'
          //        ^^^^ insert
          yield fixer.insertTextAfter(importToken, ' type');
        } else {
          const commaToken = nullThrows(
            context.sourceCode.getTokenAfter(defaultSpecifier, isCommaToken),
            NullThrowsReasons.MissingToken(',', defaultSpecifier.type),
          );
          // import Type , {...} from 'foo'
          //        ^^^^^ pick
          const defaultText = context.sourceCode.text
            .slice(defaultSpecifier.range[0], commaToken.range[0])
            .trim();
          yield fixer.insertTextBefore(
            node,
            `import type ${defaultText} from ${context.sourceCode.getText(
              node.source,
            )};\n`,
          );
          const afterToken = nullThrows(
            context.sourceCode.getTokenAfter(commaToken, {
              includeComments: true,
            }),
            NullThrowsReasons.MissingToken('any token', node.type),
          );
          // import Type , {...} from 'foo'
          //        ^^^^^^^ remove
          yield fixer.removeRange([
            defaultSpecifier.range[0],
            afterToken.range[0],
          ]);
        }
      }

      yield* fixesNamedSpecifiers.removeTypeNamedSpecifiers;
      yield* fixesRemoveTypeNamespaceSpecifier;

      yield* afterFixes;
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `report: ReportValueImport`
  - `sourceImports: SourceImports`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `classifySpecifier`
  - `fixInsertTypeSpecifierForImportDeclaration`
  - `report.typeSpecifiers.includes`
  - `fixInlineTypeImportDeclaration`
  - `namedSpecifiers.some`
  - `namedSpecifiers.every`
  - `namedSpecifiers.filter`
  - `getFixesNamedSpecifiers`
  - `fixInsertNamedSpecifiersInNamedSpecifierList`
  - `afterFixes.push`
  - `fixer.insertTextBefore`
  - `typeNamedSpecifiers
                .map(spec => {
                  const insertText = context.sourceCode.text.slice(
                    ...spec.range,
                  );
                  return `type ${insertText}`;
                })
                .join`
  - `context.sourceCode.getText`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenBefore`
  - `NullThrowsReasons.MissingToken`
  - `fixesRemoveTypeNamespaceSpecifier.push`
  - `fixer.removeRange`
  - `context.sourceCode.getFirstToken`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getTokenAfter`
  - `context.sourceCode.text
            .slice(defaultSpecifier.range[0], commaToken.range[0])
            .trim`
- **Internal Comments**:
```
// import * as types from 'foo'
// checks for presence of import assertions
// import Type from 'foo' (x2)
// if there is a default specifier but it isn't a type specifier, then just add the inline type modifier to the named specifiers (x2)
// import AValue, {BValue, Type1, Type2} from 'foo' (x2)
// import {AValue, Type1, Type2} from 'foo' (x2)
// import {Type1, Type2} from 'foo' (x2)
// The import is both default and named.  Insert named on new line because can't mix default type import and named type imports
// eslint-disable-next-line no-lonely-if
// import Foo, * as Type from 'foo' (x2)
// import DefType, * as Type from 'foo' (x4)
// import Def, * as Ns from 'foo' (x4)
//           ^^^^^^^^^ remove (x4)
// import type * as Ns from 'foo' (x2)
// ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ insert (x2)
// import type Type from 'foo' (x2)
//        ^^^^ insert (x2)
// import Type , {...} from 'foo' (x4)
//        ^^^^^ pick (x2)
//        ^^^^^^^ remove (x2)
```

### `fixInsertTypeSpecifierForImportDeclaration(fixer: TSESLint.RuleFixer, node: TSESTree.ImportDeclaration, isDefaultImport: boolean): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixInsertTypeSpecifierForImportDeclaration(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.ImportDeclaration,
      isDefaultImport: boolean,
    ): IterableIterator<TSESLint.RuleFix> {
      // import type Foo from 'foo'
      //       ^^^^^ insert
      const importToken = nullThrows(
        context.sourceCode.getFirstToken(node, isImportKeyword),
        NullThrowsReasons.MissingToken('import', node.type),
      );
      yield fixer.insertTextAfter(importToken, ' type');

      if (isDefaultImport) {
        // Has default import
        const openingBraceToken = context.sourceCode.getFirstTokenBetween(
          importToken,
          node.source,
          isOpeningBraceToken,
        );
        if (openingBraceToken) {
          // Only braces. e.g. import Foo, {} from 'foo'
          const commaToken = nullThrows(
            context.sourceCode.getTokenBefore(openingBraceToken, isCommaToken),
            NullThrowsReasons.MissingToken(',', node.type),
          );
          const closingBraceToken = nullThrows(
            context.sourceCode.getFirstTokenBetween(
              openingBraceToken,
              node.source,
              isClosingBraceToken,
            ),
            NullThrowsReasons.MissingToken('}', node.type),
          );

          // import type Foo, {} from 'foo'
          //                  ^^ remove
          yield fixer.removeRange([
            commaToken.range[0],
            closingBraceToken.range[1],
          ]);
          const specifiersText = context.sourceCode.text.slice(
            commaToken.range[1],
            closingBraceToken.range[1],
          );
          if (node.specifiers.length > 1) {
            yield fixer.insertTextAfter(
              node,
              `\nimport type${specifiersText} from ${context.sourceCode.getText(
                node.source,
              )};`,
            );
          }
        }
      }

      // make sure we don't do anything like `import type {type T} from 'foo';`
      for (const specifier of node.specifiers) {
        if (
          specifier.type === AST_NODE_TYPES.ImportSpecifier &&
          specifier.importKind === 'type'
        ) {
          yield* fixRemoveTypeSpecifierFromImportSpecifier(fixer, specifier);
        }
      }
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.ImportDeclaration`
  - `isDefaultImport: boolean`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `fixer.insertTextAfter`
  - `context.sourceCode.getFirstTokenBetween`
  - `context.sourceCode.getTokenBefore`
  - `fixer.removeRange`
  - `context.sourceCode.text.slice`
  - `context.sourceCode.getText`
  - `fixRemoveTypeSpecifierFromImportSpecifier`
- **Internal Comments**:
```
// import type Foo from 'foo' (x2)
//       ^^^^^ insert (x2)
// Has default import (x2)
// Only braces. e.g. import Foo, {} from 'foo' (x2)
// import type Foo, {} from 'foo' (x2)
//                  ^^ remove (x2)
// make sure we don't do anything like `import type {type T} from 'foo';`
```

### `fixRemoveTypeSpecifierFromImportDeclaration(fixer: TSESLint.RuleFixer, node: TSESTree.ImportDeclaration): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixRemoveTypeSpecifierFromImportDeclaration(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.ImportDeclaration,
    ): IterableIterator<TSESLint.RuleFix> {
      // import type Foo from 'foo'
      //        ^^^^ remove
      const importToken = nullThrows(
        context.sourceCode.getFirstToken(node, isImportKeyword),
        NullThrowsReasons.MissingToken('import', node.type),
      );
      const typeToken = nullThrows(
        context.sourceCode.getFirstTokenBetween(
          importToken,
          node.specifiers[0]?.local ?? node.source,
          isTypeKeyword,
        ),
        NullThrowsReasons.MissingToken('type', node.type),
      );
      const afterToken = nullThrows(
        context.sourceCode.getTokenAfter(typeToken, { includeComments: true }),
        NullThrowsReasons.MissingToken('any token', node.type),
      );
      yield fixer.removeRange([typeToken.range[0], afterToken.range[0]]);
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.ImportDeclaration`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getFirstTokenBetween`
  - `context.sourceCode.getTokenAfter`
  - `fixer.removeRange`
- **Internal Comments**:
```
// import type Foo from 'foo' (x2)
//        ^^^^ remove (x2)
```

### `fixRemoveTypeSpecifierFromImportSpecifier(fixer: TSESLint.RuleFixer, node: TSESTree.ImportSpecifier): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixRemoveTypeSpecifierFromImportSpecifier(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.ImportSpecifier,
    ): IterableIterator<TSESLint.RuleFix> {
      // import { type Foo } from 'foo'
      //          ^^^^ remove
      const typeToken = nullThrows(
        context.sourceCode.getFirstToken(node, isTypeKeyword),
        NullThrowsReasons.MissingToken('type', node.type),
      );
      const afterToken = nullThrows(
        context.sourceCode.getTokenAfter(typeToken, { includeComments: true }),
        NullThrowsReasons.MissingToken('any token', node.type),
      );
      yield fixer.removeRange([typeToken.range[0], afterToken.range[0]]);
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.ImportSpecifier`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `context.sourceCode.getTokenAfter`
  - `fixer.removeRange`
- **Internal Comments**:
```
// import { type Foo } from 'foo' (x2)
//          ^^^^ remove (x2)
```


---

## Interfaces

### `SourceImports`

<details><summary>Interface Code</summary>

```ts
interface SourceImports {
  reportValueImports: ReportValueImport[];
  source: string;
  // ImportDeclaration for type-only import only with named imports.
  typeOnlyNamedImport: TSESTree.ImportDeclaration | null;
  // ImportDeclaration for value-only import only with default imports and/or named imports.
  valueImport: TSESTree.ImportDeclaration | null;
  // ImportDeclaration for value-only import only with named imports.
  valueOnlyNamedImport: TSESTree.ImportDeclaration | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `reportValueImports` | `ReportValueImport[]` | ✗ |  |
| `source` | `string` | ✗ |  |
| `typeOnlyNamedImport` | `TSESTree.ImportDeclaration | null` | ✗ |  |
| `valueImport` | `TSESTree.ImportDeclaration | null` | ✗ |  |
| `valueOnlyNamedImport` | `TSESTree.ImportDeclaration | null` | ✗ |  |

### `ReportValueImport`

<details><summary>Interface Code</summary>

```ts
interface ReportValueImport {
  inlineTypeSpecifiers: TSESTree.ImportSpecifier[];
  node: TSESTree.ImportDeclaration;
  typeSpecifiers: TSESTree.ImportClause[]; // It has at least one element.
  unusedSpecifiers: TSESTree.ImportClause[];
  valueSpecifiers: TSESTree.ImportClause[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `inlineTypeSpecifiers` | `TSESTree.ImportSpecifier[]` | ✗ |  |
| `node` | `TSESTree.ImportDeclaration` | ✗ |  |
| `typeSpecifiers` | `TSESTree.ImportClause[]` | ✗ |  |
| `unusedSpecifiers` | `TSESTree.ImportClause[]` | ✗ |  |
| `valueSpecifiers` | `TSESTree.ImportClause[]` | ✗ |  |


---

## Type Aliases

### `Prefer`

```ts
type Prefer = 'no-type-imports' | 'type-imports';
```

### `FixStyle`

```ts
type FixStyle = 'inline-type-imports' | 'separate-type-imports';
```

### `Options`

```ts
type Options = [
  {
    disallowTypeAnnotations?: boolean;
    fixStyle?: FixStyle;
    prefer?: Prefer;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'avoidImportType'
  | 'noImportTypeAnnotations'
  | 'someImportsAreOnlyTypes'
  | 'typeOverValue';
```


---