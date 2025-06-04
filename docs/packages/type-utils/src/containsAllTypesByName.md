[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `containsAllTypesByName.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/containsAllTypesByName.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isTypeFlagSet` | `./typeFlagUtils` |


---

## Functions

### `containsAllTypesByName(type: ts.Type, allowAny: boolean, allowedNames: Set<string>, matchAnyInstead: boolean): boolean`

<details><summary>Code</summary>

```ts
export function containsAllTypesByName(
  type: ts.Type,
  allowAny: boolean,
  allowedNames: Set<string>,
  matchAnyInstead = false,
): boolean {
  if (isTypeFlagSet(type, ts.TypeFlags.Any | ts.TypeFlags.Unknown)) {
    return !allowAny;
  }

  if (tsutils.isTypeReference(type)) {
    type = type.target;
  }

  const symbol = type.getSymbol();
  if (symbol && allowedNames.has(symbol.name)) {
    return true;
  }

  const predicate = (t: ts.Type): boolean =>
    containsAllTypesByName(t, allowAny, allowedNames, matchAnyInstead);

  if (tsutils.isUnionOrIntersectionType(type)) {
    return matchAnyInstead
      ? type.types.some(predicate)
      : type.types.every(predicate);
  }

  const bases = type.getBaseTypes();

  return (
    bases != null &&
    (matchAnyInstead
      ? bases.some(predicate)
      : bases.length > 0 && bases.every(predicate))
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param type Type being checked by name.
 * @param allowAny Whether to consider `any` and `unknown` to match.
 * @param allowedNames Symbol names checking on the type.
 * @param matchAnyInstead Whether to instead just check if any parts match, rather than all parts.
 * @returns Whether the type is, extends, or contains the allowed names (or all matches the allowed names, if mustMatchAll is true).
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `allowAny: boolean`
  - `allowedNames: Set<string>`
  - `matchAnyInstead: boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
  - `tsutils.isTypeReference`
  - `type.getSymbol`
  - `allowedNames.has`
  - `containsAllTypesByName`
  - `tsutils.isUnionOrIntersectionType`
  - `type.types.some`
  - `type.types.every`
  - `type.getBaseTypes`
  - `bases.some`
  - `bases.every`
### `predicate(t: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(t: ts.Type): boolean =>
    containsAllTypesByName(t, allowAny, allowedNames, matchAnyInstead)
```
</details>

- **Parameters**:
  - `t: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `containsAllTypesByName`

---