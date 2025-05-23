[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `removeSourceCodeNotice.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---