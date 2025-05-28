[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertRuleDescription.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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