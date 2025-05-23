[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unused-expressions.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `RuleTestCaseError`

```ts
type RuleTestCaseError = Omit<TestCaseError<string>, 'messageId'>;
```


---