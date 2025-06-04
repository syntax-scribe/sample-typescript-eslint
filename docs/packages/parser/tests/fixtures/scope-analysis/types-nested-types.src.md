[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types-nested-types.src.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/types-nested-types.src.ts`**

## Type Aliases

### `Foo`

```ts
type Foo = | [number, string?, boolean?]
  | ([{}, [number?] | (null & boolean[])] & {});
```


---