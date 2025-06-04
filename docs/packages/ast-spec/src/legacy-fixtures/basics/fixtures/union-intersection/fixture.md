[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 4 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/union-intersection/fixture.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `union` | `number | null | undefined` | let/var | `*not shown*` | ✗ |
| `intersection` | `number & string` | let/var | `*not shown*` | ✗ |
| `precedence1` | `number | (string & boolean)` | let/var | `*not shown*` | ✗ |
| `precedence2` | `(number & string) | boolean` | let/var | `*not shown*` | ✗ |


---


---

## Type Aliases

### `unionLeading`

```ts
type unionLeading = number | string;
```

### `intersectionLeading`

```ts
type intersectionLeading = number & string;
```

### `unionLeadingSingle`

```ts
type unionLeadingSingle = number;
```

### `intersectionLeadingSingle`

```ts
type intersectionLeadingSingle = number;
```


---