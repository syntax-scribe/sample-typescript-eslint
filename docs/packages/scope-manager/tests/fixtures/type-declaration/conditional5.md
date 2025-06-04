[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional5.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional5.ts`**

## Type Aliases

### `Test<U>`

```ts
type Test<U> = U extends (arg: { [k: string]: (arg2: infer I) => void }) => void
  ? I
  : never;
```


---