[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional-nested.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional-nested.ts`**

## Type Aliases

### `Test<T>`

```ts
type Test<T> = T extends Array<infer U> ? U : T extends Set<infer U> ? U : never;
```


---