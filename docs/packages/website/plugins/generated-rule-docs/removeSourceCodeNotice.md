[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `removeSourceCodeNotice.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
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