[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/conditional-infer-nested/fixture.ts`**

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