[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useRulesMeta.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useRulesMeta.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RulesMeta` | `@site/rulesMeta` |
| `useDocusaurusContext` | `@docusaurus/useDocusaurusContext` |


---

## Functions

### `useRulesMeta(): RulesMeta`

<details><summary>Code</summary>

```ts
export function useRulesMeta(): RulesMeta {
  const {
    siteConfig: { customFields },
  } = useDocusaurusContext();
  if (!customFields) {
    throw new Error('Custom fields not found in config');
  }
  return customFields.rules as RulesMeta;
}
```
</details>

- **Return Type**: `RulesMeta`
- **Calls**:
  - `useDocusaurusContext (from @docusaurus/useDocusaurusContext)`

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