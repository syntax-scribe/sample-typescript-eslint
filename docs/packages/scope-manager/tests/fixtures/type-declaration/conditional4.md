[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `conditional4.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/conditional4.ts`**

## Type Aliases

### `Test<U>`

```ts
type Test<U> = U extends { [k: string]: infer I } ? I : never;
```


---