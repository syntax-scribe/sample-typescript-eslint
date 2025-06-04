[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `dot-notation.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/dot-notation.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/dot-notation` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |


---

## Functions

### `q(str: string): string`

<details><summary>Code</summary>

```ts
function q(str: string): string {
  return `"${str}"`;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Quote a string in "double quotes" because it’s painful
 * with a double-quoted string literal
 */
```

- **Parameters**:
  - `str: string`
- **Return Type**: `string`

---