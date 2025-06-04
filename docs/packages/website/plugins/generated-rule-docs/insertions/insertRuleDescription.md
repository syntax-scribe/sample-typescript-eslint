[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertRuleDescription.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertRuleDescription.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MdxJsxFlowElement` | `mdast-util-mdx` |
| `RuleDocsPage` | `../RuleDocsPage` |


---

## Functions

### `insertRuleDescription(page: RuleDocsPage): void`

<details><summary>Code</summary>

```ts
export function insertRuleDescription(page: RuleDocsPage): void {
  page.spliceChildren(0, 0, `> ${page.rule.meta.docs.description}.`, {
    attributes: [
      {
        name: 'name',
        type: 'mdxJsxAttribute',
        value: page.file.stem,
      },
    ],
    name: 'RuleAttributes',
    type: 'mdxJsxFlowElement',
  } as MdxJsxFlowElement);
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `void`
- **Calls**:
  - `page.spliceChildren`

---