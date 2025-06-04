[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `infer-type-constraint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/infer-type-constraint.ts`**

## Type Aliases

### `X`

```ts
type X = string | number;
```

### `Id<T>`

```ts
type Id<T> = T extends { id: infer Id extends X } ? Id : never;
```


---