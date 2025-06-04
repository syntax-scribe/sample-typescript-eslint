[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 5 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/conditional-infer-with-constraint/fixture.ts`**


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