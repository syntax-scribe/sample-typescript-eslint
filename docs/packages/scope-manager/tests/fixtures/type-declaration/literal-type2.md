[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `literal-type2.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/fixtures/type-declaration/literal-type2.ts`**

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