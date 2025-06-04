[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `switch-exhaustiveness-check.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 11 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/switch-exhaustiveness-check.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `isClosingBraceToken` | `../util` |
| `isOpeningBraceToken` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `requiresQuoting` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_COMMENT_PATTERN` | `RegExp` | const | `/^no default$/iu` | ✗ |
| `commentRegExp` | `RegExp` | const | `defaultCaseCommentPattern != null
        ? new RegExp(defaultCaseCommentPattern, 'u')
        : DEFAULT_COMMENT_PATTERN` | ✗ |
| `commentsAfterLastCase` | `any` | const | `lastCase
        ? context.sourceCode.getCommentsAfter(lastCase)
        : []` | ✗ |
| `symbolName` | `string` | const | `discriminantType.getSymbol()?.escapedName as
        | string
        | undefined` | ✗ |
| `caseTypes` | `Set<ts.Type>` | const | `new Set<ts.Type>()` | ✗ |
| `missingLiteralBranchTypes` | `ts.Type[]` | const | `[]` | ✗ |
| `lastCase` | `any` | const | `node.cases.length > 0 ? node.cases[node.cases.length - 1] : null` | ✗ |
| `caseIndent` | `string` | const | `lastCase
        ? ' '.repeat(lastCase.loc.start.column)
        : // If there are no cases, use indentation of the switch statement and
          // leave it to the user to format it correctly.
          ' '.repeat(node.loc.start.column)` | ✗ |
| `missingCases` | `any[]` | const | `[]` | ✗ |
| `missingBranchName` | `any` | const | `missingBranchType.getSymbol()?.escapedName` | ✗ |
| `caseTest` | `any` | let/var | `tsutils.isTypeFlagSet(
          missingBranchType,
          ts.TypeFlags.ESSymbolLike,
        )
          ? // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
            missingBranchName!
          : typeToString(missingBranchType)` | ✗ |


---

## Functions

### `getCommentDefaultCase(node: TSESTree.SwitchStatement): TSESTree.Comment | undefined`

<details><summary>Code</summary>

```ts
function getCommentDefaultCase(
      node: TSESTree.SwitchStatement,
    ): TSESTree.Comment | undefined {
      const lastCase = node.cases.at(-1);
      const commentsAfterLastCase = lastCase
        ? context.sourceCode.getCommentsAfter(lastCase)
        : [];
      const defaultCaseComment = commentsAfterLastCase.at(-1);

      if (commentRegExp.test(defaultCaseComment?.value.trim() || '')) {
        return defaultCaseComment;
      }

      return;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SwitchStatement`
- **Return Type**: `TSESTree.Comment | undefined`
- **Calls**:
  - `node.cases.at`
  - `context.sourceCode.getCommentsAfter`
  - `commentsAfterLastCase.at`
  - `commentRegExp.test`
  - `defaultCaseComment?.value.trim`
### `typeToString(type: ts.Type): string`

<details><summary>Code</summary>

```ts
function typeToString(type: ts.Type): string {
      return checker.typeToString(
        type,
        undefined,
        ts.TypeFormatFlags.AllowUniqueESSymbolType |
          ts.TypeFormatFlags.UseAliasDefinedOutsideCurrentScope |
          ts.TypeFormatFlags.UseFullyQualifiedType,
      );
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `checker.typeToString`
### `getSwitchMetadata(node: TSESTree.SwitchStatement): SwitchMetadata`

<details><summary>Code</summary>

```ts
function getSwitchMetadata(node: TSESTree.SwitchStatement): SwitchMetadata {
      const defaultCase = node.cases.find(
        switchCase => switchCase.test == null,
      );

      const discriminantType = getConstrainedTypeAtLocation(
        services,
        node.discriminant,
      );

      const symbolName = discriminantType.getSymbol()?.escapedName as
        | string
        | undefined;

      const containsNonLiteralType =
        doesTypeContainNonLiteralType(discriminantType);

      const caseTypes = new Set<ts.Type>();
      for (const switchCase of node.cases) {
        // If the `test` property of the switch case is `null`, then we are on a
        // `default` case.
        if (switchCase.test == null) {
          continue;
        }

        const caseType = getConstrainedTypeAtLocation(
          services,
          switchCase.test,
        );
        caseTypes.add(caseType);
      }

      const missingLiteralBranchTypes: ts.Type[] = [];

      for (const unionPart of tsutils.unionConstituents(discriminantType)) {
        for (const intersectionPart of tsutils.intersectionConstituents(
          unionPart,
        )) {
          if (
            caseTypes.has(intersectionPart) ||
            !isTypeLiteralLikeType(intersectionPart)
          ) {
            continue;
          }

          // "missing", "optional" and "undefined" types are different runtime objects,
          // but all of them have TypeFlags.Undefined type flag
          if (
            [...caseTypes].some(tsutils.isIntrinsicUndefinedType) &&
            tsutils.isIntrinsicUndefinedType(intersectionPart)
          ) {
            continue;
          }

          missingLiteralBranchTypes.push(intersectionPart);
        }
      }

      return {
        containsNonLiteralType,
        defaultCase: defaultCase ?? getCommentDefaultCase(node),
        missingLiteralBranchTypes,
        symbolName,
      };
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SwitchStatement`
- **Return Type**: `SwitchMetadata`
- **Calls**:
  - `node.cases.find`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `discriminantType.getSymbol`
  - `doesTypeContainNonLiteralType`
  - `caseTypes.add`
  - `tsutils.unionConstituents`
  - `tsutils.intersectionConstituents`
  - `caseTypes.has`
  - `isTypeLiteralLikeType`
  - `[...caseTypes].some`
  - `tsutils.isIntrinsicUndefinedType`
  - `missingLiteralBranchTypes.push`
  - `getCommentDefaultCase`
- **Internal Comments**:
```
// If the `test` property of the switch case is `null`, then we are on a
// `default` case.
// "missing", "optional" and "undefined" types are different runtime objects,
// but all of them have TypeFlags.Undefined type flag
```

### `checkSwitchExhaustive(node: TSESTree.SwitchStatement, switchMetadata: SwitchMetadata): void`

<details><summary>Code</summary>

```ts
function checkSwitchExhaustive(
      node: TSESTree.SwitchStatement,
      switchMetadata: SwitchMetadata,
    ): void {
      const { defaultCase, missingLiteralBranchTypes, symbolName } =
        switchMetadata;

      // If considerDefaultExhaustiveForUnions is enabled, the presence of a default case
      // always makes the switch exhaustive.
      if (considerDefaultExhaustiveForUnions && defaultCase != null) {
        return;
      }

      if (missingLiteralBranchTypes.length > 0) {
        context.report({
          node: node.discriminant,
          messageId: 'switchIsNotExhaustive',
          data: {
            missingBranches: missingLiteralBranchTypes
              .map(missingType =>
                tsutils.isTypeFlagSet(missingType, ts.TypeFlags.ESSymbolLike)
                  ? `typeof ${missingType.getSymbol()?.escapedName as string}`
                  : typeToString(missingType),
              )
              .join(' | '),
          },
          suggest: [
            {
              messageId: 'addMissingCases',
              fix(fixer): TSESLint.RuleFix | null {
                return fixSwitch(
                  fixer,
                  node,
                  missingLiteralBranchTypes,
                  defaultCase,
                  symbolName?.toString(),
                );
              },
            },
          ],
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SwitchStatement`
  - `switchMetadata: SwitchMetadata`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `missingLiteralBranchTypes
              .map(missingType =>
                tsutils.isTypeFlagSet(missingType, ts.TypeFlags.ESSymbolLike)
                  ? `typeof ${missingType.getSymbol()?.escapedName as string}`
                  : typeToString(missingType),
              )
              .join`
  - `fixSwitch`
  - `symbolName?.toString`
- **Internal Comments**:
```
// If considerDefaultExhaustiveForUnions is enabled, the presence of a default case
// always makes the switch exhaustive.
```

### `fixSwitch(fixer: TSESLint.RuleFixer, node: TSESTree.SwitchStatement, missingBranchTypes: (ts.Type | null)[], defaultCase: TSESTree.Comment | TSESTree.SwitchCase | undefined, symbolName: string): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
function fixSwitch(
      fixer: TSESLint.RuleFixer,
      node: TSESTree.SwitchStatement,
      missingBranchTypes: (ts.Type | null)[], // null means default branch
      defaultCase: TSESTree.Comment | TSESTree.SwitchCase | undefined,
      symbolName?: string,
    ): TSESLint.RuleFix {
      const lastCase =
        node.cases.length > 0 ? node.cases[node.cases.length - 1] : null;

      const caseIndent = lastCase
        ? ' '.repeat(lastCase.loc.start.column)
        : // If there are no cases, use indentation of the switch statement and
          // leave it to the user to format it correctly.
          ' '.repeat(node.loc.start.column);

      const missingCases = [];
      for (const missingBranchType of missingBranchTypes) {
        if (missingBranchType == null) {
          missingCases.push(`default: { throw new Error('default case') }`);
          continue;
        }

        const missingBranchName = missingBranchType.getSymbol()?.escapedName;
        let caseTest = tsutils.isTypeFlagSet(
          missingBranchType,
          ts.TypeFlags.ESSymbolLike,
        )
          ? // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
            missingBranchName!
          : typeToString(missingBranchType);

        if (
          symbolName &&
          (missingBranchName || missingBranchName === '') &&
          requiresQuoting(missingBranchName.toString(), compilerOptions.target)
        ) {
          const escapedBranchName = missingBranchName
            .replaceAll("'", "\\'")
            .replaceAll('\n', '\\n')
            .replaceAll('\r', '\\r');

          caseTest = `${symbolName}['${escapedBranchName}']`;
        }

        missingCases.push(
          `case ${caseTest}: { throw new Error('Not implemented yet: ${caseTest
            .replaceAll('\\', '\\\\')
            .replaceAll("'", "\\'")} case') }`,
        );
      }

      const fixString = missingCases
        .map(code => `${caseIndent}${code}`)
        .join('\n');

      if (lastCase) {
        if (defaultCase) {
          const beforeFixString = missingCases
            .map(code => `${code}\n${caseIndent}`)
            .join('');

          return fixer.insertTextBefore(defaultCase, beforeFixString);
        }
        return fixer.insertTextAfter(lastCase, `\n${fixString}`);
      }

      // There were no existing cases.
      const openingBrace = nullThrows(
        context.sourceCode.getTokenAfter(
          node.discriminant,
          isOpeningBraceToken,
        ),
        NullThrowsReasons.MissingToken('{', 'discriminant'),
      );
      const closingBrace = nullThrows(
        context.sourceCode.getTokenAfter(
          node.discriminant,
          isClosingBraceToken,
        ),
        NullThrowsReasons.MissingToken('}', 'discriminant'),
      );

      return fixer.replaceTextRange(
        [openingBrace.range[0], closingBrace.range[1]],
        ['{', fixString, `${caseIndent}}`].join('\n'),
      );
    }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
  - `node: TSESTree.SwitchStatement`
  - `missingBranchTypes: (ts.Type | null)[]`
  - `defaultCase: TSESTree.Comment | TSESTree.SwitchCase | undefined`
  - `symbolName: string`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `' '.repeat`
  - `missingCases.push`
  - `missingBranchType.getSymbol`
  - `tsutils.isTypeFlagSet`
  - `typeToString`
  - `requiresQuoting (from ../util)`
  - `missingBranchName.toString`
  - `missingBranchName
            .replaceAll("'", "\\'")
            .replaceAll('\n', '\\n')
            .replaceAll`
  - `caseTest
            .replaceAll('\\', '\\\\')
            .replaceAll`
  - `missingCases
        .map(code => `${caseIndent}${code}`)
        .join`
  - `missingCases
            .map(code => `${code}\n${caseIndent}`)
            .join`
  - `fixer.insertTextBefore`
  - `fixer.insertTextAfter`
  - `nullThrows (from ../util)`
  - `context.sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `fixer.replaceTextRange`
  - `['{', fixString, `${caseIndent}}`].join`
- **Internal Comments**:
```
// leave it to the user to format it correctly. (x3)
// There were no existing cases. (x2)
```

### `checkSwitchUnnecessaryDefaultCase(switchMetadata: SwitchMetadata): void`

<details><summary>Code</summary>

```ts
function checkSwitchUnnecessaryDefaultCase(
      switchMetadata: SwitchMetadata,
    ): void {
      if (allowDefaultCaseForExhaustiveSwitch) {
        return;
      }

      const { containsNonLiteralType, defaultCase, missingLiteralBranchTypes } =
        switchMetadata;

      if (
        missingLiteralBranchTypes.length === 0 &&
        defaultCase != null &&
        !containsNonLiteralType
      ) {
        context.report({
          node: defaultCase,
          messageId: 'dangerousDefaultCase',
        });
      }
    }
```
</details>

- **Parameters**:
  - `switchMetadata: SwitchMetadata`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `checkSwitchNoUnionDefaultCase(node: TSESTree.SwitchStatement, switchMetadata: SwitchMetadata): void`

<details><summary>Code</summary>

```ts
function checkSwitchNoUnionDefaultCase(
      node: TSESTree.SwitchStatement,
      switchMetadata: SwitchMetadata,
    ): void {
      if (!requireDefaultForNonUnion) {
        return;
      }

      const { containsNonLiteralType, defaultCase } = switchMetadata;

      if (containsNonLiteralType && defaultCase == null) {
        context.report({
          node: node.discriminant,
          messageId: 'switchIsNotExhaustive',
          data: { missingBranches: 'default' },
          suggest: [
            {
              messageId: 'addMissingCases',
              fix(fixer): TSESLint.RuleFix {
                return fixSwitch(fixer, node, [null], defaultCase);
              },
            },
          ],
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.SwitchStatement`
  - `switchMetadata: SwitchMetadata`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `fixSwitch`
### `isTypeLiteralLikeType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isTypeLiteralLikeType(type: ts.Type): boolean {
  return tsutils.isTypeFlagSet(
    type,
    ts.TypeFlags.Literal |
      ts.TypeFlags.Undefined |
      ts.TypeFlags.Null |
      ts.TypeFlags.UniqueESSymbol,
  );
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.isTypeFlagSet`
### `doesTypeContainNonLiteralType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function doesTypeContainNonLiteralType(type: ts.Type): boolean {
  return tsutils
    .unionConstituents(type)
    .some(type =>
      tsutils
        .intersectionConstituents(type)
        .every(subType => !isTypeLiteralLikeType(subType)),
    );
}
```
</details>

- **JSDoc**:
```ts
/**
 * For example:
 *
 * - `"foo" | "bar"` is a type with all literal types.
 * - `"foo" | number` is a type that contains non-literal types.
 * - `"foo" & { bar: 1 }` is a type that contains non-literal types.
 *
 * Default cases are never superfluous in switches with non-literal types.
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
    .unionConstituents(type)
    .some`
  - `tsutils
        .intersectionConstituents(type)
        .every`
  - `isTypeLiteralLikeType`

---

## Interfaces

### `SwitchMetadata`

<details><summary>Interface Code</summary>

```ts
interface SwitchMetadata {
  readonly containsNonLiteralType: boolean;
  readonly defaultCase: TSESTree.Comment | TSESTree.SwitchCase | undefined;
  readonly missingLiteralBranchTypes: ts.Type[];
  readonly symbolName: string | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `containsNonLiteralType` | `boolean` | ✗ |  |
| `defaultCase` | `TSESTree.Comment | TSESTree.SwitchCase | undefined` | ✗ |  |
| `missingLiteralBranchTypes` | `ts.Type[]` | ✗ |  |
| `symbolName` | `string | undefined` | ✗ |  |


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    /**
     * If `true`, allow `default` cases on switch statements with exhaustive
     * cases.
     *
     * @default true
     */
    allowDefaultCaseForExhaustiveSwitch?: boolean;

    /**
     * If `true`, require a `default` clause for switches on non-union types.
     *
     * @default false
     */
    requireDefaultForNonUnion?: boolean;

    /**
     * Regular expression for a comment that can indicate an intentionally omitted default case.
     */
    defaultCaseCommentPattern?: string;

    /**
     * If `true`, the `default` clause is used to determine whether the switch statement is exhaustive for union types.
     *
     * @default false
     */
    considerDefaultExhaustiveForUnions?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = | 'addMissingCases'
  | 'dangerousDefaultCase'
  | 'switchIsNotExhaustive';
```


---