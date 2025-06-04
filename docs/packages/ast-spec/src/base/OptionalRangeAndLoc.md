[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `OptionalRangeAndLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/OptionalRangeAndLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Range` | `./Range` |
| `SourceLocation` | `./SourceLocation` |


---

## Type Aliases

### `OptionalRangeAndLoc<T>`

```ts
type OptionalRangeAndLoc<T> = {
  loc?: SourceLocation;
  range?: Range;
} & Pick<T, Exclude<keyof T, 'loc' | 'range'>>;
```


---