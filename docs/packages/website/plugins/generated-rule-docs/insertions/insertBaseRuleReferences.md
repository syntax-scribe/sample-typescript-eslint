[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertBaseRuleReferences.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertBaseRuleReferences.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MdxJsxFlowElement` | `mdast-util-mdx` |
| `RuleDocsPage` | `../RuleDocsPage` |
| `convertToPlaygroundHash` | `../../utils/rules` |
| `getRulesString` | `../../utils/rules` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `extendsBaseRuleName` | `any` | const | `typeof page.rule.meta.docs.extendsBaseRule === 'string'
      ? page.rule.meta.docs.extendsBaseRule
      : page.file.stem` | ✗ |
| `eslintrc` | `string` | const | ``{
  "rules": ${getRulesString(extendsBaseRuleName, page.file.stem, false)}
}`` | ✗ |


---

## Functions

### `insertBaseRuleReferences(page: RuleDocsPage): string`

<details><summary>Code</summary>

```ts
export function insertBaseRuleReferences(page: RuleDocsPage): string {
  const extendsBaseRuleName =
    typeof page.rule.meta.docs.extendsBaseRule === 'string'
      ? page.rule.meta.docs.extendsBaseRule
      : page.file.stem;

  page.spliceChildren(
    page.headingIndices.options + 1,
    0,
    `See [\`eslint/${extendsBaseRuleName}\`'s options](https://eslint.org/docs/rules/${extendsBaseRuleName}#options).`,
  );

  const eslintrc = `{
  "rules": ${getRulesString(extendsBaseRuleName, page.file.stem, false)}
}`;
  const eslintrcHash = convertToPlaygroundHash(eslintrc);

  page.spliceChildren(
    page.headingIndices.howToUse + 1,
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
              value: `export default tseslint.config({
  rules: ${getRulesString(extendsBaseRuleName, page.file.stem, true)}
});`,
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
              value: `module.exports = {
  "rules": ${getRulesString(extendsBaseRuleName, page.file.stem, true)}
};`,
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
          value: eslintrcHash,
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

  return eslintrc;
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `string`
- **Calls**:
  - `page.spliceChildren`
  - `getRulesString (from ../../utils/rules)`
  - `convertToPlaygroundHash (from ../../utils/rules)`

---