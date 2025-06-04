[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 4 |

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