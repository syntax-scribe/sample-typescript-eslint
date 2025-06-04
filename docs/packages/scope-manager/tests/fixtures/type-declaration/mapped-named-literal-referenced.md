[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `mapped-named-literal-referenced.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/mapped-named-literal-referenced.ts`**

## Type Aliases

### `T`

```ts
type T = 1;
```

### `M`

```ts
type M = { [K in string as T]: 1 };
```


---