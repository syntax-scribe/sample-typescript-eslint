[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `specifierNameMatches.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/specifierNameMatches.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `symbol` | `any` | const | `type.aliasSymbol ?? type.getSymbol()` | ✗ |
| `candidateNames` | `any[]` | const | `symbol
    ? [symbol.escapedName as string, type.intrinsicName]
    : [type.intrinsicName]` | ✗ |


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