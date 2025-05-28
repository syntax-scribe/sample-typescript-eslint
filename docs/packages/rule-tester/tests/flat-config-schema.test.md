[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `flat-config-schema.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 51 |
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
📂 **`packages/rule-tester/tests/flat-config-schema.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ObjectLike` | `../src/utils/flat-config-schema` |
| `flatConfigSchema` | `../src/utils/flat-config-schema` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `first` | `{ foo: number; }` | const | `{ foo: 42 }` | ✗ |
| `second` | `{ bar: string; }` | const | `{ bar: 'baz' }` | ✗ |
| `first` | `{ bar: string; foo: number; }` | const | `{ bar: 'baz', foo: 42 }` | ✗ |
| `second` | `{ bar: string; foo: number; }` | const | `{ bar: 'baz', foo: 42 }` | ✗ |
| `first` | `Set<string>` | const | `new Set(['bar', 'foo'])` | ✗ |
| `second` | `Set<string>` | const | `new Set(['baz'])` | ✗ |
| `first` | `{ foo: { bar: string; }; }` | const | `{ foo: { bar: 'baz' } }` | ✗ |
| `second` | `{ foo: { qux: number; }; }` | const | `{ foo: { qux: 42 } }` | ✗ |
| `first` | `{ someProperty: { 1: string; bar: string; }; }` | const | `{ someProperty: { 1: 'foo', bar: 'baz' } }` | ✗ |
| `second` | `{ someProperty: string[]; }` | const | `{ someProperty: ['qux'] }` | ✗ |
| `first` | `{ someProperty: string[]; }` | const | `{ someProperty: ['foo', 'bar', undefined, 'baz'] }` | ✗ |
| `second` | `{ someProperty: (string | number)[]; }` | const | `{ someProperty: ['qux', undefined, 42] }` | ✗ |
| `first` | `{ foo: string[]; }` | const | `{ foo: ['foobar'] }` | ✗ |
| `second` | `{ foo: { 1: string; bar: string; }; }` | const | `{ foo: { 1: 'qux', bar: 'baz' } }` | ✗ |
| `first` | `ObjectLike` | const | `{ foo: { bar: 'baz' } }` | ✗ |
| `second` | `ObjectLike` | const | `{ foo: undefined }` | ✗ |
| `first` | `{ foo: number; }` | const | `{ foo: 42 }` | ✗ |
| `second` | `{ __proto__: { qux: boolean; }; bar: string; }` | const | `{ ['__proto__']: { qux: true }, bar: 'baz' }` | ✗ |
| `first` | `{ __proto__: { foo: number; }; }` | const | `{ ['__proto__']: { foo: 42 } }` | ✗ |
| `second` | `{ __proto__: { bar: string; }; }` | const | `{ ['__proto__']: { bar: 'baz' } }` | ✗ |
| `first` | `{ foo: { bar: string; }; }` | const | `{ foo: { bar: 'baz' } }` | ✗ |
| `second` | `{ foo: any; }` | const | `{ foo: null }` | ✗ |
| `first` | `{ foo: { bar: string; }; }` | const | `{ foo: { bar: 'baz' } }` | ✗ |
| `second` | `{ foo: number; }` | const | `{ foo: 42 }` | ✗ |
| `first` | `{ foo: { bar: string; }; }` | const | `{ foo: { bar: 'baz' } }` | ✗ |
| `second` | `{ foo: string; }` | const | `{ foo: 'qux' }` | ✗ |
| `first` | `{ someProperty: { foo: number; }; }` | const | `{ someProperty: { foo: 42 } }` | ✗ |
| `second` | `{ someProperty(): void; }` | const | `{ someProperty(): void {} }` | ✗ |
| `first` | `{ someProperty: (() => void) & { foo: string; }; }` | const | `{ someProperty: Object.assign(() => {}, { foo: 'bar' }) }` | ✗ |
| `second` | `{ someProperty: { baz: string; }; }` | const | `{ someProperty: { baz: 'qux' } }` | ✗ |
| `first` | `{ bar: any; foo: any; }` | const | `{ bar: undefined, foo: undefined }` | ✗ |
| `second` | `{ baz: any; foo: any; }` | const | `{ baz: undefined, foo: undefined }` | ✗ |
| `first` | `{ __proto__: { inherited1: string; }; included1: string; notMerged1: { first: boolean; }; }` | const | `{
      __proto__: { inherited1: 'A' }, // non-own properties are not considered
      included1: 'B',
      notMerged1: { first: true },
    }` | ✗ |
| `second` | `{ __proto__: { inherited2: string; }; included2: string; notMerged2: { second: boolean; }; }` | const | `{
      __proto__: { inherited2: 'C' }, // non-own properties are not considered
      included2: 'D',
      notMerged2: { second: true },
    }` | ✗ |
| `first` | `ObjectLike` | const | `{ foo: 42 }` | ✗ |
| `second` | `ObjectLike` | const | `{ bar: 'baz' }` | ✗ |
| `expected` | `ObjectLike` | const | `{ bar: 'baz', foo: 42 }` | ✗ |
| `first` | `ObjectLike` | const | `{ foo: 42 }` | ✗ |
| `second` | `ObjectLike` | const | `{ bar: 'baz' }` | ✗ |
| `expected` | `ObjectLike` | const | `{ bar: 'baz', foo: 42 }` | ✗ |
| `first` | `ObjectLike` | const | `{ foo: 42 }` | ✗ |
| `second` | `ObjectLike` | const | `{ bar: 'baz' }` | ✗ |
| `expected` | `ObjectLike` | const | `{ bar: 'baz', foo: 42 }` | ✗ |
| `first` | `ObjectLike` | const | `{ foo: 42 }` | ✗ |
| `second` | `ObjectLike` | const | `{ bar: 'baz' }` | ✗ |
| `expected` | `{ bar: string; foo: number; reference: { bar: string; foo: number; }; }` | const | `{
      bar: 'baz',
      foo: 42,
      reference: { bar: 'baz', foo: 42 },
    }` | ✗ |
| `firstCommon` | `{ foo: number; }` | const | `{ foo: 42 }` | ✗ |
| `secondCommon` | `{ bar: string; }` | const | `{ bar: 'baz' }` | ✗ |
| `first` | `{ a: { foo: number; }; b: { foo: number; }; c: { foo: string; }; d: { foo: number; }; }` | const | `{
      a: firstCommon,
      b: firstCommon,
      c: { foo: 'different' },
      d: firstCommon,
    }` | ✗ |
| `second` | `{ a: { bar: string; }; b: { bar: string; }; c: { bar: string; }; d: { bar: string; }; }` | const | `{
      a: secondCommon,
      b: { bar: 'something else' },
      c: secondCommon,
      d: secondCommon,
    }` | ✗ |
| `expected` | `{ a: { bar: string; foo: number; }; b: { bar: string; foo: number; }; c: { bar: string; foo: string; }; d: { bar: string; foo: number; }; }` | const | `{
      a: { bar: 'baz', foo: 42 },
      b: { bar: 'something else', foo: 42 },
      c: { bar: 'baz', foo: 'different' },
      d: { bar: 'baz', foo: 42 },
    }` | ✗ |


---

## 🔧 Functions

> No functions found in this file.


---