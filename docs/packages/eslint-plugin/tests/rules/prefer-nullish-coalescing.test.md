[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-nullish-coalescing.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---