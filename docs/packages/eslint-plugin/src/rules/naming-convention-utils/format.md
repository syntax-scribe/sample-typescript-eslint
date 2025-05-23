[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `format.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 9
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/format.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `PredefinedFormats` | `./enums` |


---

## Functions

### `isPascalCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isPascalCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name[0] === name[0].toUpperCase() && !name.includes('_'))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name[0].toUpperCase`
  - `name.includes`
### `isStrictPascalCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isStrictPascalCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name[0] === name[0].toUpperCase() && hasStrictCamelHumps(name, true))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name[0].toUpperCase`
  - `hasStrictCamelHumps`
### `isCamelCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isCamelCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name[0] === name[0].toLowerCase() && !name.includes('_'))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name[0].toLowerCase`
  - `name.includes`
### `isStrictCamelCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isStrictCamelCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name[0] === name[0].toLowerCase() && hasStrictCamelHumps(name, false))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name[0].toLowerCase`
  - `hasStrictCamelHumps`
### `hasStrictCamelHumps(name: string, isUpper: boolean): boolean`

<details><summary>Code</summary>

```ts
function hasStrictCamelHumps(name: string, isUpper: boolean): boolean {
  function isUppercaseChar(char: string): boolean {
    return char === char.toUpperCase() && char !== char.toLowerCase();
  }

  if (name.startsWith('_')) {
    return false;
  }
  for (let i = 1; i < name.length; ++i) {
    if (name[i] === '_') {
      return false;
    }
    if (isUpper === isUppercaseChar(name[i])) {
      if (isUpper) {
        return false;
      }
    } else {
      isUpper = !isUpper;
    }
  }
  return true;
}
```
</details>

- **Parameters**:
  - `name: string`
  - `isUpper: boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `char.toUpperCase`
  - `char.toLowerCase`
  - `name.startsWith`
  - `isUppercaseChar`
### `isUppercaseChar(char: string): boolean`

<details><summary>Code</summary>

```ts
function isUppercaseChar(char: string): boolean {
    return char === char.toUpperCase() && char !== char.toLowerCase();
  }
```
</details>

- **Parameters**:
  - `char: string`
- **Return Type**: `boolean`
- **Calls**:
  - `char.toUpperCase`
  - `char.toLowerCase`
### `isSnakeCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isSnakeCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name === name.toLowerCase() && validateUnderscores(name))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name.toLowerCase`
  - `validateUnderscores`
### `isUpperCase(name: string): boolean`

<details><summary>Code</summary>

```ts
function isUpperCase(name: string): boolean {
  return (
    name.length === 0 ||
    (name === name.toUpperCase() && validateUnderscores(name))
  );
}
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name.toUpperCase`
  - `validateUnderscores`
### `validateUnderscores(name: string): boolean`

<details><summary>Code</summary>

```ts
function validateUnderscores(name: string): boolean {
  if (name.startsWith('_')) {
    return false;
  }
  let wasUnderscore = false;
  for (let i = 1; i < name.length; ++i) {
    if (name[i] === '_') {
      if (wasUnderscore) {
        return false;
      }
      wasUnderscore = true;
    } else {
      wasUnderscore = false;
    }
  }
  return !wasUnderscore;
}
```
</details>

- **JSDoc**:
```ts
/** Check for leading trailing and adjacent underscores */
```

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `name.startsWith`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---