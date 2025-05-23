[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `version-check.ts`

## 📚 Table of Contents

- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/version-check.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `semverCheck(version: string): boolean`

<details><summary>Code</summary>

```ts
function semverCheck(version: string): boolean {
  return semver.satisfies(
    ts.version,
    `>= ${version}.0 || >= ${version}.1-rc || >= ${version}.0-beta`,
    {
      includePrerelease: true,
    },
  );
}
```
</details>

- **Parameters**:
  - `version: string`
- **Return Type**: `boolean`
- **Calls**:
  - `semver.satisfies`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Versions`

```ts
type Versions = typeof versions extends ArrayLike<infer U> ? U : never;
```


---