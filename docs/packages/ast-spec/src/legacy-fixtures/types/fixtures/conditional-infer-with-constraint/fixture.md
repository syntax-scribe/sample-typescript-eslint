[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 5

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/conditional-infer-with-constraint/fixture.ts`**

## 📦 Imports

> No imports found in this file.


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

### `X3<T>`

```ts
type X3<T> = T extends [infer U extends number] ? MustBeNumber<U> : never;
```

### `X4<T>`

```ts
type X4<T> = T extends [infer U extends number, infer U extends number]
  ? MustBeNumber<U>
  : never;
```

### `X5<T>`

```ts
type X5<T> = T extends [infer U extends number, infer U]
  ? MustBeNumber<U>
  : never;
```

### `X6<T>`

```ts
type X6<T> = T extends [infer U, infer U extends number]
  ? MustBeNumber<U>
  : never;
```

### `X7<T>`

```ts
type X7<T> = T extends [infer U extends string, infer U extends number]
  ? U
  : never;
```


---