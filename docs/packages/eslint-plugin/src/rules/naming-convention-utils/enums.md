[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `enums.ts`

## 📚 Table of Contents

- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 7

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/enums.ts`**

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

### `PredefinedFormatsString`

```ts
type PredefinedFormatsString = keyof typeof PredefinedFormats;
```

### `UnderscoreOptionsString`

```ts
type UnderscoreOptionsString = keyof typeof UnderscoreOptions;
```

### `SelectorsString`

```ts
type SelectorsString = keyof typeof Selectors;
```

### `MetaSelectorsString`

```ts
type MetaSelectorsString = keyof typeof MetaSelectors;
```

### `IndividualAndMetaSelectorsString`

```ts
type IndividualAndMetaSelectorsString = | MetaSelectorsString
  | SelectorsString;
```

### `ModifiersString`

```ts
type ModifiersString = keyof typeof Modifiers;
```

### `TypeModifiersString`

```ts
type TypeModifiersString = keyof typeof TypeModifiers;
```


---