[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/conditional-infer-simple/fixture.ts`**

## Type Aliases

### `Foo<T>`

```ts
type Foo<T> = T extends { a: infer U; b: infer U } ? U : never;
```


---