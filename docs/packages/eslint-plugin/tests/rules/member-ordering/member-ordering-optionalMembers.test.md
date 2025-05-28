[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `member-ordering-optionalMembers.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/member-ordering/member-ordering-optionalMembers.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RunTests` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../../src/rules/member-ordering` |
| `Options` | `../../../src/rules/member-ordering` |
| `rule` | `../../../src/rules/member-ordering` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |
| `grouped` | `RunTests<MessageIds, Options>` | const | `{
  valid: [
    // optionalityOrder - required-first
    {
      code: `
interface X {
  c: string;
  b?: string;
  d?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  b?: string;
  c?: string;
  d?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
interface X {
  b: string;
  c: string;
  d: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class X {
  c: string;
  d: string;
  ['a']?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
class X {
  c: string;
  public static d: string;
  public static ['a']?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
class X {
  a: string;
  b: string;
  static {}
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
class X {
  a: string;
  [i: number]: string;
  b?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  a: string;
  [i?: number]: string;
  b?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  a: string;
  (a: number): string;
  new (i: number): string;
  b?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    // optionalityOrder - optional-first
    {
      code: `
interface X {
  b?: string;
  d?: string;
  c: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  b?: string;
  c?: string;
  d?: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
interface X {
  b: string;
  c: string;
  d: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class X {
  ['c']?: string;
  a: string;
  b: string;
}
      `,
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'alphabetically',
          },
        },
      ],
    },
  ],
  // optionalityOrder - required-first
  invalid: [
    {
      code: `
interface X {
  m: string;
  d?: string;
  b?: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            beforeMember: 'd',
            member: 'b',
          },
          line: 5,
          messageId: 'incorrectOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  a: string;
  b?: string;
  c: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            member: 'b',
            optionalOrRequired: 'required',
          },
          line: 4,
          messageId: 'incorrectRequiredMembersOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: ['call-signature', 'field', 'method'],
            optionalityOrder: 'required-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class X {
  a?: string;
  static {}
  b?: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            member: 'a',
            optionalOrRequired: 'required',
          },
          line: 3,
          messageId: 'incorrectRequiredMembersOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class X {
  b: string;
  a: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            beforeMember: 'b',
            member: 'a',
            optionalOrRequired: 'required',
          },
          line: 4,
          messageId: 'incorrectOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'required-first',
            order: 'natural-case-insensitive',
          },
        },
      ],
    },
    // optionalityOrder - optional-first
    {
      code: `
interface X {
  d?: string;
  b?: string;
  m: string;
}
      `,
      errors: [
        {
          column: 3,
          line: 4,
          messageId: 'incorrectOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'alphabetically',
          },
        },
      ],
    },
    {
      code: `
interface X {
  a?: string;
  b: string;
  c?: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            member: 'b',
            optionalOrRequired: 'optional',
          },
          line: 4,
          messageId: 'incorrectRequiredMembersOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: ['call-signature', 'field', 'method'],
            optionalityOrder: 'optional-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class Test {
  a?: string;
  b?: string;
  f: string;
  c?: string;
  d?: string;
  g: string;
  h: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            member: 'f',
            optionalOrRequired: 'optional',
          },
          line: 5,
          messageId: 'incorrectRequiredMembersOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'as-written',
          },
        },
      ],
    },
    {
      code: `
class Test {
  a: string;
  b: string;
  f?: string;
  c?: string;
  d?: string;
}
      `,
      errors: [
        {
          column: 3,
          data: {
            member: 'a',
            optionalOrRequired: 'optional',
          },
          line: 3,
          messageId: 'incorrectRequiredMembersOrder',
        },
      ],
      options: [
        {
          default: {
            memberTypes: 'never',
            optionalityOrder: 'optional-first',
            order: 'as-written',
          },
        },
      ],
    },
  ],
}` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---