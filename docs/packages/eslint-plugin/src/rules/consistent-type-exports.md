[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-exports.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 11 |
| 📊 Variables & Constants | 11 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/consistent-type-exports.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `formatWordList` | `../util` |
| `getParserServices` | `../util` |
| `isClosingBraceToken` | `../util` |
| `isOpeningBraceToken` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `sourceExportsMap` | `Record<string, SourceExports>` | const | `{}` | ✗ |
| `aliasedSymbol` | `any` | const | `tsutils.isSymbolFlagSet(
        symbol,
        ts.SymbolFlags.Alias,
      )
        ? checker.getAliasedSymbol(symbol)
        : symbol` | ✗ |
| `source` | `string` | const | `getSourceFromExport(node) ?? 'undefined'` | ✗ |
| `sourceExports` | `SourceExports` | const | `(sourceExportsMap[source] ||= {
          reportValueExports: [],
          source,
          typeOnlyNamedExport: null,
          valueOnlyNamedExport: null,
        })` | ✗ |
| `typeBasedSpecifiers` | `TSESTree.ExportSpecifier[]` | const | `[]` | ✗ |
| `inlineTypeSpecifiers` | `TSESTree.ExportSpecifier[]` | const | `[]` | ✗ |
| `valueSpecifiers` | `TSESTree.ExportSpecifier[]` | const | `[]` | ✗ |
| `exportNames` | `any` | const | `allExportNames[0]` | ✗ |
| `typeSpecifiers` | `any[]` | let/var | `[...typeBasedSpecifiers, ...inlineTypeSpecifiers]` | ✗ |
| `exportedName` | `any` | const | `specifier.exported.type === AST_NODE_TYPES.Literal
      ? specifier.exported.raw
      : specifier.exported.name` | ✗ |
| `localName` | `any` | const | `specifier.local.type === AST_NODE_TYPES.Literal
      ? specifier.local.raw
      : specifier.local.name` | ✗ |


---

## Functions

### `isSymbolTypeBased(symbol: ts.Symbol | undefined): boolean | undefined`

<details><summary>Code</summary>

```ts
function isSymbolTypeBased(
      symbol: ts.Symbol | undefined,
    ): boolean | undefined {
      if (!symbol) {
        return undefined;
      }

      const aliasedSymbol = tsutils.isSymbolFlagSet(
        symbol,
        ts.SymbolFlags.Alias,
      )
        ? checker.getAliasedSymbol(symbol)
        : symbol;

      if (checker.isUnknownSymbol(aliasedSymbol)) {
        return undefined;
      }

      return !(aliasedSymbol.flags & ts.SymbolFlags.Value);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Helper for identifying if a symbol resolves to a
     * JavaScript value or a TypeScript type.
     *
     * @returns True/false if is a type or not, or undefined if the specifier
     * can't be resolved.
     */
```

- **Parameters**:
  - `symbol: ts.Symbol | undefined`
- **Return Type**: `boolean | undefined`
- **Calls**:
  - `tsutils.isSymbolFlagSet`
  - `checker.getAliasedSymbol`
  - `checker.isUnknownSymbol`
### `fixExportInsertType(fixer: TSESLint.RuleFixer, sourceCode: Readonly<TSESLint.SourceCode>, node: TSESTree.ExportNamedDeclaration): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixExportInsertType(
  fixer: TSESLint.RuleFixer,
  sourceCode: Readonly<TSESLint.SourceCode>,
  node: TSESTree.ExportNamedDeclaration,
): IterableIterator<TSESLint.RuleFix> {
  const exportToken = nullThrows(
    sourceCode.getFirstToken(node),
    NullThrowsReasons.MissingToken('export', node.type),
  );

  yield fixer.insertTextAfter(exportToken, ' type');

  for (const specifier of node.specifiers) {
    if (specifier.exportKind === 'type') {
      const kindToken = nullThrows(
        sourceCode.getFirstToken(specifier),
        NullThrowsReasons.MissingToken('export', specifier.type),
      );
      const firstTokenAfter = nullThrows(
        sourceCode.getTokenAfter(kindToken, {
          includeComments: true,
        }),
        'Missing token following the export kind.',
      );

      yield fixer.removeRange([kindToken.range[0], firstTokenAfter.range[0]]);
    }
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Inserts "type" into an export.
 *
 * Example:
 *
 * export type { Foo } from 'foo';
 *        ^^^^
 */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `sourceCode: Readonly<TSESLint.SourceCode>`
  - `node: TSESTree.ExportNamedDeclaration`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `nullThrows (from ../util)`
  - `sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `fixer.insertTextAfter`
  - `sourceCode.getTokenAfter`
  - `fixer.removeRange`
### `fixSeparateNamedExports(fixer: TSESLint.RuleFixer, sourceCode: Readonly<TSESLint.SourceCode>, report: ReportValueExport): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixSeparateNamedExports(
  fixer: TSESLint.RuleFixer,
  sourceCode: Readonly<TSESLint.SourceCode>,
  report: ReportValueExport,
): IterableIterator<TSESLint.RuleFix> {
  const { node, inlineTypeSpecifiers, typeBasedSpecifiers, valueSpecifiers } =
    report;
  const typeSpecifiers = [...typeBasedSpecifiers, ...inlineTypeSpecifiers];
  const source = getSourceFromExport(node);
  const specifierNames = typeSpecifiers.map(getSpecifierText).join(', ');

  const exportToken = nullThrows(
    sourceCode.getFirstToken(node),
    NullThrowsReasons.MissingToken('export', node.type),
  );

  // Filter the bad exports from the current line.
  const filteredSpecifierNames = valueSpecifiers
    .map(getSpecifierText)
    .join(', ');
  const openToken = nullThrows(
    sourceCode.getFirstToken(node, isOpeningBraceToken),
    NullThrowsReasons.MissingToken('{', node.type),
  );
  const closeToken = nullThrows(
    sourceCode.getLastToken(node, isClosingBraceToken),
    NullThrowsReasons.MissingToken('}', node.type),
  );

  // Remove exports from the current line which we're going to re-insert.
  yield fixer.replaceTextRange(
    [openToken.range[1], closeToken.range[0]],
    ` ${filteredSpecifierNames} `,
  );

  // Insert the bad exports into a new export line above.
  yield fixer.insertTextBefore(
    exportToken,
    `export type { ${specifierNames} }${source ? ` from '${source}'` : ''};\n`,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Separates the exports which mismatch the kind of export the given
 * node represents. For example, a type export's named specifiers which
 * represent values will be inserted in a separate `export` statement.
 */
```

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `sourceCode: Readonly<TSESLint.SourceCode>`
  - `report: ReportValueExport`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `getSourceFromExport`
  - `typeSpecifiers.map(getSpecifierText).join`
  - `nullThrows (from ../util)`
  - `sourceCode.getFirstToken`
  - `NullThrowsReasons.MissingToken`
  - `valueSpecifiers
    .map(getSpecifierText)
    .join`
  - `sourceCode.getLastToken`
  - `fixer.replaceTextRange`
  - `fixer.insertTextBefore`
- **Internal Comments**:
```
// Filter the bad exports from the current line. (x2)
// Remove exports from the current line which we're going to re-insert. (x2)
// Insert the bad exports into a new export line above. (x2)
```

### `fixAddTypeSpecifierToNamedExports(fixer: TSESLint.RuleFixer, report: ReportValueExport): IterableIterator<TSESLint.RuleFix>`

<details><summary>Code</summary>

```ts
function* fixAddTypeSpecifierToNamedExports(
  fixer: TSESLint.RuleFixer,
  report: ReportValueExport,
): IterableIterator<TSESLint.RuleFix> {
  if (report.node.exportKind === 'type') {
    return;
  }

  for (const specifier of report.typeBasedSpecifiers) {
    yield fixer.insertTextBefore(specifier, 'type ');
  }
}
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `report: ReportValueExport`
- **Return Type**: `IterableIterator<TSESLint.RuleFix>`
- **Calls**:
  - `fixer.insertTextBefore`
### `getSourceFromExport(node: TSESTree.ExportNamedDeclaration): string | undefined`

<details><summary>Code</summary>

```ts
function getSourceFromExport(
  node: TSESTree.ExportNamedDeclaration,
): string | undefined {
  if (
    node.source?.type === AST_NODE_TYPES.Literal &&
    typeof node.source.value === 'string'
  ) {
    return node.source.value;
  }

  return undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the source of the export, or undefined if the named export has no source.
 */
```

- **Parameters**:
  - `node: TSESTree.ExportNamedDeclaration`
- **Return Type**: `string | undefined`
### `getSpecifierText(specifier: TSESTree.ExportSpecifier): string`

<details><summary>Code</summary>

```ts
function getSpecifierText(specifier: TSESTree.ExportSpecifier): string {
  const exportedName =
    specifier.exported.type === AST_NODE_TYPES.Literal
      ? specifier.exported.raw
      : specifier.exported.name;
  const localName =
    specifier.local.type === AST_NODE_TYPES.Literal
      ? specifier.local.raw
      : specifier.local.name;

  return `${localName}${
    exportedName !== localName ? ` as ${exportedName}` : ''
  }`;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the specifier text for the export. If it is aliased, we take care to return
 * the proper formatting.
 */
```

- **Parameters**:
  - `specifier: TSESTree.ExportSpecifier`
- **Return Type**: `string`

---

## Interfaces

### `SourceExports`

<details><summary>Interface Code</summary>

```ts
interface SourceExports {
  reportValueExports: ReportValueExport[];
  source: string;
  typeOnlyNamedExport: TSESTree.ExportNamedDeclaration | null;
  valueOnlyNamedExport: TSESTree.ExportNamedDeclaration | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `reportValueExports` | `ReportValueExport[]` | ✗ |  |
| `source` | `string` | ✗ |  |
| `typeOnlyNamedExport` | `TSESTree.ExportNamedDeclaration | null` | ✗ |  |
| `valueOnlyNamedExport` | `TSESTree.ExportNamedDeclaration | null` | ✗ |  |

### `ReportValueExport`

<details><summary>Interface Code</summary>

```ts
interface ReportValueExport {
  inlineTypeSpecifiers: TSESTree.ExportSpecifier[];
  node: TSESTree.ExportNamedDeclaration;
  typeBasedSpecifiers: TSESTree.ExportSpecifier[];
  valueSpecifiers: TSESTree.ExportSpecifier[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `inlineTypeSpecifiers` | `TSESTree.ExportSpecifier[]` | ✗ |  |
| `node` | `TSESTree.ExportNamedDeclaration` | ✗ |  |
| `typeBasedSpecifiers` | `TSESTree.ExportSpecifier[]` | ✗ |  |
| `valueSpecifiers` | `TSESTree.ExportSpecifier[]` | ✗ |  |


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    fixMixedExportsWithInlineTypeSpecifier: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'multipleExportsAreTypes'
  | 'singleExportIsType'
  | 'typeOverValue';
```


---