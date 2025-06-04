[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/legacy-fixtures/types/fixtures/template-literal-type-4/fixture.ts`**

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