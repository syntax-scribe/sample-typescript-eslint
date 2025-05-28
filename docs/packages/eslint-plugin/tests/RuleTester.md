[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `RuleTester.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 5 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/RuleTester.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `ValidTestCase` | `@typescript-eslint/rule-tester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `lineOffset` | `1 | 2` | const | `options.code.startsWith('\n') ? 2 : 1` | ✗ |
| `output` | `any` | const | `'output' in options && options.output
      ? options.output.trim().split('\n')
      : null` | ✗ |
| `lineNum` | `any` | const | `i + lineOffset` | ✗ |
| `errors` | `any` | const | `'errors' in options
          ? options.errors.filter(e => e.line === lineNum)
          : []` | ✗ |
| `returnVal` | `any` | const | `{
        ...options,
        code,
        errors: errors.map(e => ({
          ...e,
          line: 1,
        })),
      }` | ✗ |


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