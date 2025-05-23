[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `RuleTester.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/RuleTester.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `ValidTestCase` | `@typescript-eslint/rule-tester` |


---

## Functions

### `getFixturesRootDir(): string`

<details><summary>Code</summary>

```ts
export function getFixturesRootDir(): string {
  return path.join(__dirname, 'fixtures');
}
```
</details>

- **Return Type**: `string`
- **Calls**:
  - `path.join`
### `batchedSingleLineTests(test: ValidTestCase<Options>): ValidTestCase<Options>[]`

<details><summary>Code</summary>

```ts
export function batchedSingleLineTests<Options extends readonly unknown[]>(
  test: ValidTestCase<Options>,
): ValidTestCase<Options>[];
```
</details>

- **JSDoc**:
```ts
/**
 * Converts a batch of single line tests into a number of separate test cases.
 * This makes it easier to write tests which use the same options.
 *
 * Why wouldn't you just leave them as one test?
 * Because it makes the test error messages harder to decipher.
 * This way each line will fail separately, instead of them all failing together.
 *
 * @deprecated - DO NOT USE THIS FOR NEW RULES
 */
```

- **Parameters**:
  - `test: ValidTestCase<Options>`
- **Return Type**: `ValidTestCase<Options>[]`

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