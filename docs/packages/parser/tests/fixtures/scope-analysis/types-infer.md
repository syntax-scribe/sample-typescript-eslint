[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types-infer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/types-infer.ts`**

## Type Aliases

### `Unpacked<T>`

```ts
type Unpacked<T> = T extends (infer U)[]
  ? U
  : T extends infer U
    ? U
    : T extends Promise<infer U>
      ? U
      : T;
```


---