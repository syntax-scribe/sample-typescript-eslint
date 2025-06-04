[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `type-query-qualified.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📊 Variables & Constants | 1 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/type-query-qualified.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `x` | `{ y: { z: number; }; }` | const | `{ y: { z: 1 } }` | ✗ |


---

## Type Aliases

### `T`

```ts
type T = typeof x.y.z;
```

### `Unresolved`

```ts
type Unresolved = x.y.z;
```


---