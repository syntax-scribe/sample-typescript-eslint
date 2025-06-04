[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/object-with-typed-methods/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `foo` | `{ constructor<T>(): number; foo<T>(): number; a: number; }` | const | `{
  constructor<T>(): number {
    return 1;
  },
  foo<T>(): number {
    return 1;
  },
  get a(): number {
    return 1;
  },
  set a(x: number): number {},
}` | ✗ |


---