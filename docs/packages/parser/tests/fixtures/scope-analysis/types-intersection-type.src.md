[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types-intersection-type.src.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/types-intersection-type.src.ts`**

## Type Aliases

### `LinkedList<T>`

```ts
type LinkedList<T> = T & { next: LinkedList<T> };
```


---