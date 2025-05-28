[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertNewRuleReferences.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 7 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 1 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertNewRuleReferences.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintPluginDocs` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `MdxJsxFlowElement` | `mdast-util-mdx` |
| `compile` | `@typescript-eslint/rule-schema-to-typescript-types` |
| `EOL` | `node:os` |
| `prettier` | `prettier` |
| `RuleDocsPage` | `../RuleDocsPage` |
| `nodeIsHeading` | `../../utils/nodes` |
| `convertToPlaygroundHash` | `../../utils/rules` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `COMPLICATED_RULE_OPTIONS` | `Set<string>` | const | `new Set([
  'member-ordering',
  'naming-convention',
])` | ✗ |
| `config` | `any` | let/var | `await prettier.resolveConfig(filepath, {
    config: PRETTIER_CONFIG_PATH,
  })` | ✗ |
| `rules` | `string` | let/var | ``{
    "@typescript-eslint/${page.file.stem}": "error"
  }`` | ✗ |
| `eslintrc` | `string` | let/var | ``{
  "rules": ${rules}
}`` | ✗ |
| `eslintConfig` | `string` | let/var | ``{
  rules: ${rules}
}`` | ✗ |
| `hasNoConfig` | `boolean` | let/var | `Array.isArray(page.rule.meta.schema)
    ? page.rule.meta.schema.length === 0
    : Object.keys(page.rule.meta.schema).length === 0` | ✗ |
| `recommended` | `any` | const | `page.rule.meta.docs.recommended` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `insertNewRuleReferences` | compile(page.rule.meta.schema, prettierConfig), prettier.format(
            getRuleDefaultOptions(page),
            await prettierConfig,
          ), prettierConfig | *none* |


---

## Functions

### `insertNewRuleReferences(page: RuleDocsPage): Promise<string>`

<details><summary>Code</summary>

```ts
export async function insertNewRuleReferences(
  page: RuleDocsPage,
): Promise<string> {
  // For non-extended rules, the code snippet is placed before the first h2
  // (i.e. at the end of the initial explanation)
  const firstH2Index = page.children.findIndex(
    child => nodeIsHeading(child) && child.depth === 2,
  );

  const rules = `{
    "@typescript-eslint/${page.file.stem}": "error"
  }`;

  const eslintrc = `{
  "rules": ${rules}
}`;

  const eslintConfig = `{
  rules: ${rules}
}`;

  page.spliceChildren(
    firstH2Index,
    0,
    {
      children: [
        {
          attributes: [
            {
              name: 'value',
              type: 'mdxJsxAttribute',
              value: 'Flat Config',
            },
          ],
          children: [
            {
              lang: 'js',
              meta: 'title="eslint.config.mjs"',
              type: 'code',
              value: `export default tseslint.config(${eslintConfig});`,
            },
          ],
          name: 'TabItem',
          type: 'mdxJsxFlowElement',
        },
        {
          attributes: [
            {
              name: 'value',
              type: 'mdxJsxAttribute',
              value: 'Legacy Config',
            },
          ],
          children: [
            {
              lang: 'js',
              meta: 'title=".eslintrc.cjs"',
              type: 'code',
              value: `module.exports = ${eslintrc};`,
            },
          ],
          name: 'TabItem',
          type: 'mdxJsxFlowElement',
        },
      ],
      name: 'Tabs',
      type: 'mdxJsxFlowElement',
    } as MdxJsxFlowElement,
    {
      attributes: [
        {
          name: 'eslintrcHash',
          type: 'mdxJsxAttribute',
          value: convertToPlaygroundHash(eslintrc),
        },
      ],
      children: [
        {
          children: [
            {
              type: 'text',
              value: 'Try this rule in the playground ↗',
            },
          ],
          type: 'paragraph',
        },
      ],
      name: 'TryInPlayground',
      type: 'mdxJsxFlowElement',
    } as MdxJsxFlowElement,
  );

  const hasNoConfig = Array.isArray(page.rule.meta.schema)
    ? page.rule.meta.schema.length === 0
    : Object.keys(page.rule.meta.schema).length === 0;

  if (hasNoConfig) {
    page.spliceChildren(
      page.headingIndices.options + 1,
      0,
      'This rule is not configurable.',
    );
  } else if (!COMPLICATED_RULE_OPTIONS.has(page.file.stem)) {
    page.spliceChildren(
      page.headingIndices.options + 1,
      0,
      typeof page.rule.meta.docs.recommended === 'object'
        ? linkToConfigsForObject(page.rule.meta.docs)
        : 'This rule accepts the following options:',
      {
        lang: 'ts',
        type: 'code',
        value: [
          await compile(page.rule.meta.schema, prettierConfig),
          await prettier.format(
            getRuleDefaultOptions(page),
            await prettierConfig,
          ),
        ]
          .join(EOL)
          .trim(),
      } as mdast.Code,
    );
  }

  return eslintrc;
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `Promise<string>`
- **Calls**:
  - `page.children.findIndex`
  - `nodeIsHeading (from ../../utils/nodes)`
  - `page.spliceChildren`
  - `convertToPlaygroundHash (from ../../utils/rules)`
  - `Array.isArray`
  - `Object.keys`
  - `COMPLICATED_RULE_OPTIONS.has`
  - `linkToConfigsForObject`
  - `[
          await compile(page.rule.meta.schema, prettierConfig),
          await prettier.format(
            getRuleDefaultOptions(page),
            await prettierConfig,
          ),
        ]
          .join(EOL)
          .trim`
- **Internal Comments**:
```
// For non-extended rules, the code snippet is placed before the first h2 (x2)
// (i.e. at the end of the initial explanation) (x2)
```

### `linkToConfigsForObject(docs: ESLintPluginDocs): string`

<details><summary>Code</summary>

```ts
function linkToConfigsForObject(docs: ESLintPluginDocs): string {
  return [
    'This rule accepts the following options, and has more strict settings in the',
    (docs.requiresTypeChecking ? ['strict', 'strict-type-checked'] : ['strict'])
      .map(config => `[${config}](/users/configs#${config})`)
      .join(' and '),
    `config${docs.requiresTypeChecking ? 's' : ''}.`,
  ].join(' ');
}
```
</details>

- **Parameters**:
  - `docs: ESLintPluginDocs`
- **Return Type**: `string`
- **Calls**:
  - `[
    'This rule accepts the following options, and has more strict settings in the',
    (docs.requiresTypeChecking ? ['strict', 'strict-type-checked'] : ['strict'])
      .map(config => `[${config}](/users/configs#${config})`)
      .join(' and '),
    `config${docs.requiresTypeChecking ? 's' : ''}.`,
  ].join`
  - `(docs.requiresTypeChecking ? ['strict', 'strict-type-checked'] : ['strict'])
      .map(config => `[${config}](/users/configs#${config})`)
      .join`
### `getRuleDefaultOptions(page: RuleDocsPage): string`

<details><summary>Code</summary>

```ts
function getRuleDefaultOptions(page: RuleDocsPage): string {
  const defaults = JSON.stringify(page.rule.defaultOptions);
  const recommended = page.rule.meta.docs.recommended;

  return typeof recommended === 'object'
    ? [
        `const defaultOptionsRecommended: Options = ${defaults};`,
        '',
        '// These options are merged on top of the recommended defaults',
        `const defaultOptionsStrict: Options = ${JSON.stringify(recommended.strict)};`,
      ].join('\n')
    : `const defaultOptions: Options = ${defaults};`;
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `string`
- **Calls**:
  - `JSON.stringify`
  - `[
        `const defaultOptionsRecommended: Options = ${defaults};`,
        '',
        '// These options are merged on top of the recommended defaults',
        `const defaultOptionsStrict: Options = ${JSON.stringify(recommended.strict)};`,
      ].join`

---