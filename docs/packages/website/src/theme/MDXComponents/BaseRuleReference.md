[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `BaseRuleReference.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/BaseRuleReference.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---