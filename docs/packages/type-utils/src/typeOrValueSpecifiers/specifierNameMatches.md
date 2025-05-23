[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `specifierNameMatches.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/specifierNameMatches.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `specifierNameMatches(type: ts.Type, names: string | string[]): boolean`

<details><summary>Code</summary>

```ts
export function specifierNameMatches(
  type: ts.Type,
  names: string | string[],
): boolean {
  if (typeof names === 'string') {
    names = [names];
  }

  const symbol = type.aliasSymbol ?? type.getSymbol();
  const candidateNames = symbol
    ? [symbol.escapedName as string, type.intrinsicName]
    : [type.intrinsicName];

  if (names.some(item => candidateNames.includes(item))) {
    return true;
  }

  return false;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `names: string | string[]`
- **Return Type**: `boolean`
- **Calls**:
  - `type.getSymbol`
  - `names.some`
  - `candidateNames.includes`

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