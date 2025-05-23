[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `typeFlagUtils.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeFlagUtils.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `getTypeFlags(type: ts.Type): ts.TypeFlags`

<details><summary>Code</summary>

```ts
export function getTypeFlags(type: ts.Type): ts.TypeFlags {
  // @ts-expect-error Since typescript 5.0, this is invalid, but uses 0 as the default value of TypeFlags.
  let flags: ts.TypeFlags = 0;
  for (const t of tsutils.unionConstituents(type)) {
    flags |= t.flags;
  }
  return flags;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets all of the type flags in a type, iterating through unions automatically.
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `ts.TypeFlags`
- **Calls**:
  - `tsutils.unionConstituents`
- **Internal Comments**:
```
// @ts-expect-error Since typescript 5.0, this is invalid, but uses 0 as the default value of TypeFlags. (x2)
```

### `isTypeFlagSet(type: ts.Type, flagsToCheck: ts.TypeFlags, isReceiver: boolean): boolean`

<details><summary>Code</summary>

```ts
export function isTypeFlagSet(
  type: ts.Type,
  flagsToCheck: ts.TypeFlags,
  /** @deprecated This params is not used and will be removed in the future.*/
  isReceiver?: boolean,
): boolean {
  const flags = getTypeFlags(type);

  // eslint-disable-next-line @typescript-eslint/no-deprecated -- not used
  if (isReceiver && flags & ANY_OR_UNKNOWN) {
    return true;
  }

  return (flags & flagsToCheck) !== 0;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @param flagsToCheck The composition of one or more `ts.TypeFlags`.
 * @param isReceiver Whether the type is a receiving type (e.g. the type of a
 * called function's parameter).
 * @remarks
 * Note that if the type is a union, this function will decompose it into the
 * parts and get the flags of every union constituent. If this is not desired,
 * use the `isTypeFlag` function from tsutils.
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `flagsToCheck: ts.TypeFlags`
  - `isReceiver: boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `getTypeFlags`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-deprecated -- not used
```


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