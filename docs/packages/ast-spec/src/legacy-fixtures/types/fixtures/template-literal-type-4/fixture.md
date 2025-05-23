[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/template-literal-type-4/fixture.ts`**

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

### `EnthusiasticGreeting<T extends string extends string>`

```ts
type EnthusiasticGreeting<T extends string extends string> = `${Uppercase<T>} - ${Lowercase<T>} - ${Capitalize<T>} - ${Uncapitalize<T>}`;
```

### `HELLO`

```ts
type HELLO = EnthusiasticGreeting<'heLLo'>;
```


---