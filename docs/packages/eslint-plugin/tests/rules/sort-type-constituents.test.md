[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `sort-type-constituents.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/sort-type-constituents.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `ValidTestCase` | `@typescript-eslint/rule-tester` |
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../src/rules/sort-type-constituents` |
| `Options` | `../../src/rules/sort-type-constituents` |
| `rule` | `../../src/rules/sort-type-constituents` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |
| `type` | `"Intersection" | "Union"` | const | `operator === '|' ? 'Union' : 'Intersection'` | ✗ |


---

## Functions

### `valid(operator: '&' | '|'): ValidTestCase<Options>[]`

<details><summary>Code</summary>

```ts
(operator: '&' | '|'): ValidTestCase<Options>[] => [
  {
    code: `type T = A ${operator} B;`,
  },
  {
    code: `type T = A ${operator} /* comment */ B;`,
  },
  {
    code: `type T = 'A' ${operator} 'B';`,
  },
  {
    code: `type T = 1 ${operator} 2;`,
  },
  {
    code: noFormat`type T = (A) ${operator} (B);`,
  },
  {
    code: `type T = { a: string } ${operator} { b: string };`,
  },
  {
    code: `type T = [1, 2, 3] ${operator} [1, 2, 4];`,
  },
  {
    code: `type T = (() => string) ${operator} (() => void);`,
  },
  {
    code: `type T = () => string ${operator} void;`,
  },
  {
    // testing the default ordering
    code: noFormat`
type T =
  ${operator} A
  ${operator} B
  ${operator} C.D
  ${operator} D.E
  ${operator} intrinsic
  ${operator} number[]
  ${operator} string[]
  ${operator} any
  ${operator} string
  ${operator} symbol
  ${operator} this
  ${operator} readonly number[]
  ${operator} readonly string[]
  ${operator} 'a'
  ${operator} 'b'
  ${operator} "a"
  ${operator} "b"
  ${operator} (() => string)
  ${operator} (() => void)
  ${operator} (new () => string)
  ${operator} (new () => void)
  ${operator} import('bar')
  ${operator} import('foo')
  ${operator} (number extends string ? unknown : never)
  ${operator} (string extends string ? unknown : never)
  ${operator} { [a in string]: string }
  ${operator} { [a: string]: string }
  ${operator} { [b in string]: string }
  ${operator} { [b: string]: string }
  ${operator} { a: string }
  ${operator} { b: string }
  ${operator} [1, 2, 3]
  ${operator} [1, 2, 4]
  ${operator} (A & B)
  ${operator} (B & C)
  ${operator} (A | B)
  ${operator} (B | C)
  ${operator} null
  ${operator} undefined
    `,
  },
]
```
</details>

- **Parameters**:
  - `operator: '&' | '|'`
- **Return Type**: `ValidTestCase<Options>[]`
### `invalid(operator: '&' | '|'): InvalidTestCase<MessageIds, Options>[]`

<details><summary>Code</summary>

```ts
(
  operator: '&' | '|',
): InvalidTestCase<MessageIds, Options>[] => {
  const type = operator === '|' ? 'Union' : 'Intersection';
  return [
    {
      code: `type T = B ${operator} A;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = A ${operator} B;`,
    },
    {
      code: `type T = 'B' ${operator} 'A';`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = 'A' ${operator} 'B';`,
    },
    {
      code: `type T = 2 ${operator} 1;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = 1 ${operator} 2;`,
    },
    {
      code: noFormat`type T = (B) ${operator} (A);`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = A ${operator} B;`,
    },
    {
      code: `type T = { b: string } ${operator} { a: string };`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = { a: string } ${operator} { b: string };`,
    },
    {
      code: `type T = [1, 2, 4] ${operator} [1, 2, 3];`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = [1, 2, 3] ${operator} [1, 2, 4];`,
    },
    {
      code: `type T = (() => void) ${operator} (() => string);`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = (() => string) ${operator} (() => void);`,
    },
    {
      code: `type T = () => void ${operator} string;`,
      errors: [
        {
          data: {
            type,
          },
          messageId: 'notSorted',
        },
      ],
      output: `type T = () => string ${operator} void;`,
    },
    {
      code: `type T = () => undefined ${operator} null;`,
      errors: [
        {
          data: {
            type,
          },
          messageId: 'notSorted',
        },
      ],
      output: `type T = () => null ${operator} undefined;`,
    },
    {
      code: noFormat`
type T =
  ${operator} [1, 2, 4]
  ${operator} [1, 2, 3]
  ${operator} { b: string }
  ${operator} { a: string }
  ${operator} (() => void)
  ${operator} (() => string)
  ${operator} "b"
  ${operator} "a"
  ${operator} 'b'
  ${operator} 'a'
  ${operator} readonly string[]
  ${operator} readonly number[]
  ${operator} string[]
  ${operator} number[]
  ${operator} D.E
  ${operator} C.D
  ${operator} B
  ${operator} A
  ${operator} undefined
  ${operator} null
  ${operator} string
  ${operator} any;
      `,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `
type T =
  A ${operator} B ${operator} C.D ${operator} D.E ${operator} number[] ${operator} string[] ${operator} any ${operator} string ${operator} readonly number[] ${operator} readonly string[] ${operator} 'a' ${operator} 'b' ${operator} "a" ${operator} "b" ${operator} (() => string) ${operator} (() => void) ${operator} { a: string } ${operator} { b: string } ${operator} [1, 2, 3] ${operator} [1, 2, 4] ${operator} null ${operator} undefined;
      `,
    },
    {
      code: `type T = B ${operator} /* comment */ A;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
          suggestions: [
            {
              messageId: 'suggestFix',
              output: `type T = A ${operator} B;`,
            },
          ],
        },
      ],
      output: null,
    },
    {
      code: `type T = (() => /* comment */ A) ${operator} B;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
          suggestions: null,
        },
      ],
      output: `type T = B ${operator} (() => /* comment */ A);`,
    },
    {
      code: `type Expected = (new (x: number) => boolean) ${operator} string;`,
      errors: [
        {
          messageId: 'notSortedNamed',
        },
      ],
      output: `type Expected = string ${operator} (new (x: number) => boolean);`,
    },
    {
      code: `type T = (| A) ${operator} B;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = B ${operator} (| A);`,
    },
    {
      code: `type T = (& A) ${operator} B;`,
      errors: [
        {
          data: {
            name: 'T',
            type,
          },
          messageId: 'notSortedNamed',
        },
      ],
      output: `type T = B ${operator} (& A);`,
    },
  ];
}
```
</details>

- **Parameters**:
  - `operator: '&' | '|'`
- **Return Type**: `InvalidTestCase<MessageIds, Options>[]`

---