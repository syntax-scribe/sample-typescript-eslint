[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `object-pattern.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/function/params/object-pattern.ts`**

## Type Aliases

### `Fn<A extends { a: string } extends { a: string }>`

```ts
type Fn<A extends { a: string } extends { a: string }> = ({ a }: A) => unknown;
```


---