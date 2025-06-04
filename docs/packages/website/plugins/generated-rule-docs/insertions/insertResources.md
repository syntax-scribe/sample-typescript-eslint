[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertResources.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertResources.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MdxJsxFlowElement` | `mdast-util-mdx` |
| `RuleDocsPage` | `../RuleDocsPage` |
| `getUrlForRuleTest` | `../../utils/rules` |
| `sourceUrlPrefix` | `../../utils/rules` |


---

## Functions

### `insertResources(page: RuleDocsPage): void`

<details><summary>Code</summary>

```ts
export function insertResources(page: RuleDocsPage): void {
  // Add a link to view the rule's source and test code
  page.spliceChildren(
    page.children.length,
    0,
    `## Resources

- [Rule source](${sourceUrlPrefix}src/rules/${page.file.stem}.ts)
- [Test source](${getUrlForRuleTest(page.file.stem)})
    `,
  );

  // Also add a notice about coming from ESLint core for extension rules
  if (page.rule.meta.docs.extendsBaseRule) {
    page.spliceChildren(page.children.length, 0, {
      attributes: [
        {
          name: 'baseRule',
          type: 'mdxJsxAttribute',
          value:
            page.rule.meta.docs.extendsBaseRule === true
              ? page.file.stem
              : page.rule.meta.docs.extendsBaseRule,
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
      name: 'BaseRuleReference',
      type: 'mdxJsxFlowElement',
    } as MdxJsxFlowElement);
  }
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `void`
- **Calls**:
  - `page.spliceChildren`
  - `getUrlForRuleTest (from ../../utils/rules)`
- **Internal Comments**:
```
// Add a link to view the rule's source and test code (x4)
// Also add a notice about coming from ESLint core for extension rules
```


---