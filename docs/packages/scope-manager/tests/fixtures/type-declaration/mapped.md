[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `mapped.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/mapped.ts`**

## Type Aliases

### `T`

```ts
type T = Record<string, string>;
```

### `A`

```ts
type A = { [k in string]: T[k] };
```


---