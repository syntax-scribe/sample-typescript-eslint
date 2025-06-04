[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `removeSourceCodeNotice.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/removeSourceCodeNotice.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleDocsPage` | `./RuleDocsPage` |


---

## Functions

### `removeSourceCodeNotice(page: RuleDocsPage): void`

<details><summary>Code</summary>

```ts
export function removeSourceCodeNotice(page: RuleDocsPage): void {
  page.spliceChildren(
    page.children.findIndex(v => v.type === 'blockquote'),
    1,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Removes " 🛑 This file is source code, not the primary documentation location! 🛑".
 */
```

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `void`
- **Calls**:
  - `page.spliceChildren`
  - `page.children.findIndex`

---