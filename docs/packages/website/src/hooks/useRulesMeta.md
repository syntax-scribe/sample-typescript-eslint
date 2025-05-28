[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useRulesMeta.ts`

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