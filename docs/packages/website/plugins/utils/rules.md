[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `rules.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/plugins/utils/rules.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintPluginRuleModule` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `RuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `VFile` | `vfile` |
| `nodeIsHeading` | `./nodes` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `sourceUrlPrefix` | `"https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/"` | const | `'https://github.com/typescript-eslint/typescript-eslint/blob/main/packages/eslint-plugin/'` | ✓ |
| `childMatch` | `(node: mdast.PhrasingContent) => boolean` | const | `typeof contents === 'string'
      ? (node: mdast.PhrasingContent): boolean =>
          node.type === 'text' && node.value === contents
      : contents` | ✗ |


---

## Functions

### `getRulesString(extendsBaseRuleName: string, stem: string, withComment: boolean): string`

<details><summary>Code</summary>

```ts
export function getRulesString(
  extendsBaseRuleName: string,
  stem: string,
  withComment: boolean,
): string {
  return `{${
    withComment
      ? '\n    // Note: you must disable the base rule as it can report incorrect errors'
      : ''
  }
    "${extendsBaseRuleName}": "off",
    "@typescript-eslint/${stem}": "error"
  }`;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param withComment Whether to include a full comment note.
 * @remarks `withComment` can't be used inside a JSON object which is needed for eslintrc in the playground
 */
```

- **Parameters**:
  - `extendsBaseRuleName: string`
  - `stem: string`
  - `withComment: boolean`
- **Return Type**: `string`
### `convertToPlaygroundHash(eslintrc: string): string`

<details><summary>Code</summary>

```ts
export function convertToPlaygroundHash(eslintrc: string): string {
  return lz.compressToEncodedURIComponent(eslintrc);
}
```
</details>

- **Parameters**:
  - `eslintrc: string`
- **Return Type**: `string`
- **Calls**:
  - `lz.compressToEncodedURIComponent`
### `getUrlForRuleTest(ruleName: string): string`

<details><summary>Code</summary>

```ts
export function getUrlForRuleTest(ruleName: string): string {
  for (const localPath of [
    `tests/rules/${ruleName}.test.ts`,
    `tests/rules/${ruleName}/`,
  ]) {
    if (fs.existsSync(`${eslintPluginDirectory}/${localPath}`)) {
      return `${sourceUrlPrefix}${localPath}`;
    }
  }

  throw new Error(`Could not find test file for ${ruleName}.`);
}
```
</details>

- **Parameters**:
  - `ruleName: string`
- **Return Type**: `string`
- **Calls**:
  - `fs.existsSync`
### `isESLintPluginRuleModule(rule: RuleModule<string, readonly unknown[]> | undefined): rule is ESLintPluginRuleModule`

<details><summary>Code</summary>

```ts
export function isESLintPluginRuleModule(
  rule: RuleModule<string, readonly unknown[]> | undefined,
): rule is ESLintPluginRuleModule {
  return !!rule?.meta.docs;
}
```
</details>

- **Parameters**:
  - `rule: RuleModule<string, readonly unknown[]> | undefined`
- **Return Type**: `rule is ESLintPluginRuleModule`
### `isVFileWithStem(file: VFile): file is VFileWithStem`

<details><summary>Code</summary>

```ts
export function isVFileWithStem(file: VFile): file is VFileWithStem {
  return !!file.stem;
}
```
</details>

- **Parameters**:
  - `file: VFile`
- **Return Type**: `file is VFileWithStem`
### `findHeadingIndex(children: readonly unist.Node[], depth: 2 | 3, contents: string | ((node: mdast.PhrasingContent) => boolean)): number`

<details><summary>Code</summary>

```ts
export function findHeadingIndex(
  children: readonly unist.Node[],
  depth: 2 | 3,
  contents: string | ((node: mdast.PhrasingContent) => boolean),
): number {
  const childMatch =
    typeof contents === 'string'
      ? (node: mdast.PhrasingContent): boolean =>
          node.type === 'text' && node.value === contents
      : contents;

  return children.findIndex(
    node =>
      nodeIsHeading(node) &&
      node.depth === depth &&
      node.children.length === 1 &&
      childMatch(node.children[0]),
  );
}
```
</details>

- **Parameters**:
  - `children: readonly unist.Node[]`
  - `depth: 2 | 3`
  - `contents: string | ((node: mdast.PhrasingContent) => boolean)`
- **Return Type**: `number`
- **Calls**:
  - `children.findIndex`
  - `nodeIsHeading (from ./nodes)`
  - `childMatch`

---

## Type Aliases

### `VFileWithStem`

```ts
type VFileWithStem = {
  stem: string;
} & VFile;
```


---