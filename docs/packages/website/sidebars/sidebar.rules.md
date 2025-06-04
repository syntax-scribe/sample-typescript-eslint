[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `sidebar.rules.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/sidebars/sidebar.rules.js`**

## Functions

### `createCategory(label: any, rules: any, additionalItems: any[]): { items: any[]; label: any; type: string; }`

<details><summary>Code</summary>

```ts
function createCategory(label, rules, additionalItems = []) {
  return {
    items: [
      ...rules.map(rule => {
        return {
          id: rule.name,
          label: rule.name,
          type: 'doc',
        };
      }),
      ...additionalItems,
    ],
    label,
    type: 'category',
  };
}
```
</details>

- **Parameters**:
  - `label: any`
  - `rules: any`
  - `additionalItems: any[]`
- **Return Type**: `{ items: any[]; label: any; type: string; }`
- **Calls**:
  - `rules.map`

---