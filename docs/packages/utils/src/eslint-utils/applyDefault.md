[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `applyDefault.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/utils/src/eslint-utils/applyDefault.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `deepMerge` | `./deepMerge` |
| `isObjectNotArray` | `./deepMerge` |


---

## Functions

### `applyDefault(defaultOptions: Readonly<Default>, userOptions: Readonly<User> | null): Default`

<details><summary>Code</summary>

```ts
export function applyDefault<
  User extends readonly unknown[],
  Default extends User,
>(
  defaultOptions: Readonly<Default>,
  userOptions: Readonly<User> | null,
): Default {
  // clone defaults
  const options = structuredClone(defaultOptions) as AsMutable<Default>;

  if (userOptions == null) {
    return options;
  }

  // For avoiding the type error
  //   `This expression is not callable. Type 'unknown' has no call signatures.ts(2349)`
  (options as unknown[]).forEach((opt: unknown, i: number) => {
    // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
    if (userOptions[i] !== undefined) {
      const userOpt = userOptions[i];

      if (isObjectNotArray(userOpt) && isObjectNotArray(opt)) {
        options[i] = deepMerge(opt, userOpt);
      } else {
        options[i] = userOpt;
      }
    }
  });

  return options;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Pure function - doesn't mutate either parameter!
 * Uses the default options and overrides with the options provided by the user
 * @param defaultOptions the defaults
 * @param userOptions the user opts
 * @returns the options with defaults
 */
```

- **Parameters**:
  - `defaultOptions: Readonly<Default>`
  - `userOptions: Readonly<User> | null`
- **Return Type**: `Default`
- **Calls**:
  - `structuredClone`
  - `(options as unknown[]).forEach`
  - `isObjectNotArray (from ./deepMerge)`
  - `deepMerge (from ./deepMerge)`
- **Internal Comments**:
```
// clone defaults (x2)
// For avoiding the type error (x4)
//   `This expression is not callable. Type 'unknown' has no call signatures.ts(2349)` (x4)
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `AsMutable<T extends readonly unknown[] extends readonly unknown[]>`

```ts
type AsMutable<T extends readonly unknown[] extends readonly unknown[]> = {
  -readonly [Key in keyof T]: T[Key];
};
```


---