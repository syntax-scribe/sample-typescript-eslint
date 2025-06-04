[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/mapped-named-type/fixture.ts`**

## Type Aliases

### `Test<T>`

```ts
type Test<T> = {
  [P in keyof T as 'a']: T[P];
};
```


---