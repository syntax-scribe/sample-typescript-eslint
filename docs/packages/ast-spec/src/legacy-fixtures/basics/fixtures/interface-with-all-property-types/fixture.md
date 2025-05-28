[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/interface-with-all-property-types/fixture.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `Foo`

<details><summary>Interface Code</summary>

```ts
interface Foo {
  baa: number;
  bar?: number;
  [bax]: string;
  [baz]?: string;
  [eee: number]: string;
  doo(): void;
  coo?(a, b, c): void;
  [loo]?(a, b, c): void;
  boo<J>(a, b, c): void;
  new (a, b?): string;
  new <F>(a, b?): string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `baa` | `number` | ✗ |  |
| `bar` | `number` | ✓ |  |
| `[bax]` | `string` | ✗ |  |
| `[baz]` | `string` | ✓ |  |


---