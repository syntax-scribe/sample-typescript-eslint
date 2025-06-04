[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/types.ts`**

## Type Aliases

### `MakeRequired<Base, Key extends keyof Base extends keyof Base>`

```ts
type MakeRequired<Base, Key extends keyof Base extends keyof Base> = Omit<Base, Key> &
  Required<Record<Key, NonNullable<Base[Key]>>>;
```

### `ValueOf<T>`

```ts
type ValueOf<T> = T[keyof T];
```


---