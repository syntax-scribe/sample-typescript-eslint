[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unused-expressions.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unused-expressions.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TestCaseError` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/no-unused-expressions` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      ecmaVersion: 6,
    },
  },
})` | ✗ |


---

## Functions

### `error(messages: RuleTestCaseError[]): any[]`

<details><summary>Code</summary>

```ts
function error(
  messages: RuleTestCaseError[],
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
): any[] {
  return messages.map(message => ({
    ...message,
    message:
      'Expected an assignment or function call and instead saw an expression.',
  }));
}
```
</details>

- **Parameters**:
  - `messages: RuleTestCaseError[]`
- **Return Type**: `any[]`
- **Calls**:
  - `messages.map`

---

## Type Aliases

### `RuleTestCaseError`

```ts
type RuleTestCaseError = Omit<TestCaseError<string>, 'messageId'>;
```


---