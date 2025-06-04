[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-nullish-coalescing.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/prefer-nullish-coalescing.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `ValidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../src/rules/prefer-nullish-coalescing` |
| `Options` | `../../src/rules/prefer-nullish-coalescing` |
| `rule` | `../../src/rules/prefer-nullish-coalescing` |
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
| `types` | `string[]` | const | `['string', 'number', 'boolean', 'object']` | ✗ |
| `nullishTypes` | `string[]` | const | `['null', 'undefined', 'null | undefined']` | ✗ |
| `ignorablePrimitiveTypes` | `string[]` | const | `['string', 'number', 'boolean', 'bigint']` | ✗ |


---

## Functions

### `typeValidTest(cb: (type: string, equals: '' | '=') => string | ValidTestCase<Options>): (string | ValidTestCase<Options>)[]`

<details><summary>Code</summary>

```ts
function typeValidTest(
  cb: (type: string, equals: '' | '=') => string | ValidTestCase<Options>,
): (string | ValidTestCase<Options>)[] {
  return [
    ...types.map(type => cb(type, '')),
    ...types.map(type => cb(type, '=')),
  ];
}
```
</details>

- **Parameters**:
  - `cb: (type: string, equals: '' | '=') => string | ValidTestCase<Options>`
- **Return Type**: `(string | ValidTestCase<Options>)[]`
- **Calls**:
  - `types.map`
  - `cb`
### `nullishTypeTest(cb: (nullish: string, type: string, equals: string) => T): T[]`

<details><summary>Code</summary>

```ts
<
  T extends
    | string
    | InvalidTestCase<MessageIds, Options>
    | ValidTestCase<Options>,
>(
  cb: (nullish: string, type: string, equals: string) => T,
): T[] =>
  nullishTypes.flatMap(nullish =>
    types.flatMap(type =>
      ['', ...(cb.length === 3 ? ['='] : [])].map(equals =>
        cb(nullish, type, equals),
      ),
    ),
  )
```
</details>

- **Parameters**:
  - `cb: (nullish: string, type: string, equals: string) => T`
- **Return Type**: `T[]`
- **Calls**:
  - `nullishTypes.flatMap`

---