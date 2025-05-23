[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-condition.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unnecessary-condition.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageId` | `../../src/rules/no-unnecessary-condition` |
| `Options` | `../../src/rules/no-unnecessary-condition` |
| `rule` | `../../src/rules/no-unnecessary-condition` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Functions

### `necessaryConditionTest(condition: string): string`

<details><summary>Code</summary>

```ts
(condition: string): string => `
declare const b1: ${condition};
declare const b2: boolean;
const t1 = b1 && b2;
`
```
</details>

- **Parameters**:
  - `condition: string`
- **Return Type**: `string`
### `unnecessaryConditionTest(condition: string, messageId: MessageId): InvalidTestCase<MessageId, Options>`

<details><summary>Code</summary>

```ts
(
  condition: string,
  messageId: MessageId,
): InvalidTestCase<MessageId, Options> => ({
  code: necessaryConditionTest(condition),
  errors: [{ column: 12, line: 4, messageId }],
})
```
</details>

- **Parameters**:
  - `condition: string`
  - `messageId: MessageId`
- **Return Type**: `InvalidTestCase<MessageId, Options>`

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