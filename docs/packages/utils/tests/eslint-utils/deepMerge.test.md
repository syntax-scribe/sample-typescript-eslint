[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deepMerge.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 6 |
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
📂 **`packages/utils/tests/eslint-utils/deepMerge.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintUtils` | `../../src` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `a` | `{}` | const | `{}` | ✗ |
| `b` | `{}` | const | `{}` | ✗ |
| `a` | `{ arrayA1: number[]; boolA1: boolean; numberA1: number; objA1: { arrayA2: number[]; boolA2: boolean; numberA2: number; objA2: {}; stringA2: string; }; stringA1: string; }` | const | `{
      arrayA1: [1, 2, 3],
      boolA1: true,
      numberA1: 1,
      objA1: {
        arrayA2: [3, 2, 1],
        boolA2: false,
        numberA2: 2,
        objA2: {},
        stringA2: 'fsda',
      },
      stringA1: 'asdf',
    }` | ✗ |
| `b` | `{ arrayB1: number[]; boolB1: boolean; numberB1: number; objB1: { arrayB2: number[]; boolB2: boolean; numberB2: number; objB2: {}; stringB2: string; }; stringB1: string; }` | const | `{
      arrayB1: [1, 2, 3],
      boolB1: true,
      numberB1: 1,
      objB1: {
        arrayB2: [3, 2, 1],
        boolB2: false,
        numberB2: 2,
        objB2: {},
        stringB2: 'fsda',
      },
      stringB1: 'asdf',
    }` | ✗ |
| `a` | `{ prop1: { prop2: string; }; }` | const | `{
      prop1: {
        prop2: 'hi',
      },
    }` | ✗ |
| `b` | `{ prop1: { prop2: string; }; }` | const | `{
      prop1: {
        prop2: 'bye',
      },
    }` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---