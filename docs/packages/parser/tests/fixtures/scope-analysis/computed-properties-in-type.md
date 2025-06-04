[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `computed-properties-in-type.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/parser/tests/fixtures/scope-analysis/computed-properties-in-type.ts`**

## Type Aliases

### `A`

```ts
type A = {
  [s1]: number;
  [s2](s1: number, s2: number): number;
};
```


---