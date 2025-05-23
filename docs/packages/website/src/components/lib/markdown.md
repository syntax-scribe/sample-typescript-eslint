[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `markdown.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 5
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/markdown.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ConfigModel` | `../types` |
| `parseESLintRC` | `./parseConfig` |


---

## Functions

### `createSummary(value: string, title: string, type: 'json' | 'ts', length: number): string`

<details><summary>Code</summary>

```ts
function createSummary(
  value: string,
  title: string,
  type: 'json' | 'ts',
  length: number,
): string {
  const code = `### ${title}\n\n\`\`\`${type}\n${value}\n\`\`\``;
  if ((code.match(/\n/g) ?? []).length > length) {
    return `<details>\n<summary>Expand</summary>\n\n${code}\n\n</details>`;
  }
  return code;
}
```
</details>

- **Parameters**:
  - `value: string`
  - `title: string`
  - `type: 'json' | 'ts'`
  - `length: number`
- **Return Type**: `string`
- **Calls**:
  - `code.match`
### `createSummaryJson(obj: string, field: string, title: string): string`

<details><summary>Code</summary>

```ts
function createSummaryJson(obj: string, field: string, title: string): string {
  if (obj && obj.length > 0) {
    return createSummary(obj, title, 'json', 10);
  }
  return '';
}
```
</details>

- **Parameters**:
  - `obj: string`
  - `field: string`
  - `title: string`
- **Return Type**: `string`
- **Calls**:
  - `createSummary`
### `generateVersionsTable(tsVersion: string): string`

<details><summary>Code</summary>

```ts
function generateVersionsTable(tsVersion: string): string {
  return [
    '| package | version |',
    '| -- | -- |',
    `| \`@typescript-eslint/eslint-plugin\` | \`${process.env.TS_ESLINT_VERSION}\` |`,
    `| \`@typescript-eslint/parser\` | \`${process.env.TS_ESLINT_VERSION}\` |`,
    `| \`TypeScript\` | \`${tsVersion}\` |`,
    `| \`ESLint\` | \`${process.env.ESLINT_VERSION}\` |`,
    `| \`node\` | \`web\` |`,
  ].join('\n');
}
```
</details>

- **Parameters**:
  - `tsVersion: string`
- **Return Type**: `string`
- **Calls**:
  - `[
    '| package | version |',
    '| -- | -- |',
    `| \`@typescript-eslint/eslint-plugin\` | \`${process.env.TS_ESLINT_VERSION}\` |`,
    `| \`@typescript-eslint/parser\` | \`${process.env.TS_ESLINT_VERSION}\` |`,
    `| \`TypeScript\` | \`${tsVersion}\` |`,
    `| \`ESLint\` | \`${process.env.ESLINT_VERSION}\` |`,
    `| \`node\` | \`web\` |`,
  ].join`
### `createMarkdown(state: ConfigModel): string`

<details><summary>Code</summary>

```ts
export function createMarkdown(state: ConfigModel): string {
  return [
    `[Playground](${document.location.toString()})`,
    createSummary(state.code, 'Code', 'ts', 30),
    createSummaryJson(state.eslintrc, 'rules', 'Eslint config'),
    createSummaryJson(state.tsconfig, 'compilerOptions', 'TypeScript config'),
    generateVersionsTable(state.ts),
  ]
    .filter(Boolean)
    .join('\n\n');
}
```
</details>

- **JSDoc**:
```ts
/**
 * Create a markdown string that user can copy and paste into an issue
 */
```

- **Parameters**:
  - `state: ConfigModel`
- **Return Type**: `string`
- **Calls**:
  - `[
    `[Playground](${document.location.toString()})`,
    createSummary(state.code, 'Code', 'ts', 30),
    createSummaryJson(state.eslintrc, 'rules', 'Eslint config'),
    createSummaryJson(state.tsconfig, 'compilerOptions', 'TypeScript config'),
    generateVersionsTable(state.ts),
  ]
    .filter(Boolean)
    .join`
### `createMarkdownParams(state: ConfigModel): string`

<details><summary>Code</summary>

```ts
export function createMarkdownParams(state: ConfigModel): string {
  const { rules } = parseESLintRC(state.eslintrc);
  const ruleKeys = Object.keys(rules);

  const onlyRuleName =
    ruleKeys.length === 1
      ? ruleKeys[0].replace('@typescript-eslint/', '')
      : 'rule name here';

  const params = {
    'eslint-config': `module.exports = ${state.eslintrc}`,
    labels: 'bug,package: eslint-plugin,triage',
    'playground-link': document.location.toString(),
    'repro-code': state.code,
    template: '01-bug-report-plugin.yaml',
    title: `Bug: [${onlyRuleName}] <short description of the issue>`,
    'typescript-config': state.tsconfig,
    versions: generateVersionsTable(state.ts),
  };

  return new URLSearchParams(params).toString();
}
```
</details>

- **JSDoc**:
```ts
/**
 * Create a URLSearchParams string for the issue template
 */
```

- **Parameters**:
  - `state: ConfigModel`
- **Return Type**: `string`
- **Calls**:
  - `parseESLintRC (from ./parseConfig)`
  - `Object.keys`
  - `ruleKeys[0].replace`
  - `document.location.toString`
  - `generateVersionsTable`
  - `new URLSearchParams(params).toString`

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