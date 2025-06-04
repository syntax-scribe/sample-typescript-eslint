[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/intersection-type/fixture.ts`**

## Type Aliases

### `LinkedList<T>`

```ts
type LinkedList<T> = T & { next: LinkedList<T> };
```


---