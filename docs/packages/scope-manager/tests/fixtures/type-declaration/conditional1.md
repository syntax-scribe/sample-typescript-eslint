[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional1.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional1.ts`**

## Type Aliases

### `T<U>`

```ts
type T<U> = U extends infer V ? V : never;
```

### `Unresolved`

```ts
type Unresolved = V;
```


---