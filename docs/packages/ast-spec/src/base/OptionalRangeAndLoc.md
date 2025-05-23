[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `OptionalRangeAndLoc.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/OptionalRangeAndLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Range` | `./Range` |
| `SourceLocation` | `./SourceLocation` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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