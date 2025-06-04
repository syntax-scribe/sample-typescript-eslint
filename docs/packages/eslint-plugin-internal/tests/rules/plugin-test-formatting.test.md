[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `plugin-test-formatting.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/tests/rules/plugin-test-formatting.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/plugin-test-formatting` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: getFixturesRootDir(),
    },
  },
})` | ✗ |
| `CODE_INDENT` | `"        "` | const | `'        '` | ✗ |
| `PARENT_INDENT` | `"      "` | const | `'      '` | ✗ |
| `lastIndex` | `number` | const | `strings.length - 1` | ✗ |
| `code` | `string` | const | `strings.slice(0, lastIndex).reduce((p, s, i) => p + s + keys[i], '') +
    strings[lastIndex]` | ✗ |


---

## Functions

### `wrap(strings: TemplateStringsArray, keys: string[]): string`

<details><summary>Code</summary>

```ts
function wrap(strings: TemplateStringsArray, ...keys: string[]): string {
  const lastIndex = strings.length - 1;
  const code =
    strings.slice(0, lastIndex).reduce((p, s, i) => p + s + keys[i], '') +
    strings[lastIndex];
  return `
ruleTester.run({
  valid: [
    {
      code: ${code},
    },
  ],
});
  `;
}
```
</details>

- **Parameters**:
  - `strings: TemplateStringsArray`
  - `keys: string[]`
- **Return Type**: `string`
- **Calls**:
  - `strings.slice(0, lastIndex).reduce`

---