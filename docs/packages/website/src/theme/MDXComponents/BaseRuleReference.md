[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `BaseRuleReference.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 2 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/BaseRuleReference.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `href` | `string` | const | ``https://github.com/eslint/eslint/blob/main/docs/src/rules/${baseRule}.md`` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `sup` | element | *none* | text: "Taken with ❤️ from", <a>, text: "." |
| `a` | element | href={href} | text: "ESLint core" |


---

## Functions

### `BaseRuleReference({
  baseRule,
}: BaseRuleReferenceProps): React.ReactNode`

<details><summary>Code</summary>

```ts
export function BaseRuleReference({
  baseRule,
}: BaseRuleReferenceProps): React.ReactNode {
  const href = `https://github.com/eslint/eslint/blob/main/docs/src/rules/${baseRule}.md`;

  return (
    <sup>
      Taken with ❤️ from <a href={href}>ESLint core</a>.
    </sup>
  );
}
```
</details>

- **Parameters**:
  - `{
  baseRule,
}: BaseRuleReferenceProps`
- **Return Type**: `React.ReactNode`

---

## Interfaces

### `BaseRuleReferenceProps`

<details><summary>Interface Code</summary>

```ts
export interface BaseRuleReferenceProps {
  baseRule: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `baseRule` | `string` | ✗ |  |


---