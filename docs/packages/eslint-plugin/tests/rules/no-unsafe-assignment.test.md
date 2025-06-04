[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-assignment.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/no-unsafe-assignment.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `InferMessageIdsTypeFromRule` | `../../src/util` |
| `InferOptionsTypeFromRule` | `../../src/util` |
| `rule` | `../../src/rules/no-unsafe-assignment` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.noImplicitThis.json',
      projectService: false,
      tsconfigRootDir: getFixturesRootDir(),
    },
  },
})` | ✗ |


---

## Functions

### `assignmentTest(tests: [string, number, number, boolean?][]): InvalidTest[]`

<details><summary>Code</summary>

```ts
(
  tests: [string, number, number, boolean?][],
): InvalidTest[] =>
  tests.flatMap(([assignment, column, endColumn, skipAssignmentExpression]) => [
    // VariableDeclaration
    {
      code: `const ${assignment}`,
      errors: [
        {
          column: column + 6,
          endColumn: endColumn + 6,
          line: 1,
          messageId: 'unsafeArrayPatternFromTuple',
        },
      ],
    },
    // AssignmentPattern
    {
      code: `function foo(${assignment}) {}`,
      errors: [
        {
          column: column + 13,
          endColumn: endColumn + 13,
          line: 1,
          messageId: 'unsafeArrayPatternFromTuple',
        },
      ],
    },
    // AssignmentExpression
    ...(skipAssignmentExpression
      ? []
      : [
          {
            code: `(${assignment})`,
            errors: [
              {
                column: column + 1,
                endColumn: endColumn + 1,
                line: 1,
                messageId: 'unsafeArrayPatternFromTuple' as const,
              },
            ],
          },
        ]),
  ])
```
</details>

- **Parameters**:
  - `tests: [string, number, number, boolean?][]`
- **Return Type**: `InvalidTest[]`
- **Calls**:
  - `tests.flatMap`

---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof rule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof rule>;
```

### `InvalidTest`

```ts
type InvalidTest = InvalidTestCase<MessageIds, Options>;
```


---