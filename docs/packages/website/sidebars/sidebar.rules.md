[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `sidebar.rules.js`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/sidebars/sidebar.rules.js`**

## 📦 Imports

> No imports found in this file.


---

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---