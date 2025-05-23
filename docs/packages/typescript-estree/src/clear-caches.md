[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `clear-caches.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/clear-caches.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clearWatchCaches` | `./create-program/getWatchProgramsForProjects` |
| `clearDefaultProjectMatchedFiles` | `./parser` |
| `clearProgramCacheOriginal` | `./parser` |
| `clearTSConfigMatchCache` | `./parseSettings/createParseSettings` |
| `clearTSServerProjectService` | `./parseSettings/createParseSettings` |
| `clearGlobCache` | `./parseSettings/resolveProjectList` |


---

## Functions

### `clearCaches(): void`

<details><summary>Code</summary>

```ts
export function clearCaches(): void {
  clearDefaultProjectMatchedFiles();
  clearProgramCacheOriginal();
  clearWatchCaches();
  clearTSConfigMatchCache();
  clearTSServerProjectService();
  clearGlobCache();
}
```
</details>

- **JSDoc**:
```ts
/**
 * Clears all of the internal caches.
 * Generally you shouldn't need or want to use this.
 * Examples of intended uses:
 * - In tests to reset parser state to keep tests isolated.
 * - In custom lint tooling that iteratively lints one project at a time to prevent OOMs.
 */
```

- **Return Type**: `void`
- **Calls**:
  - `clearDefaultProjectMatchedFiles (from ./parser)`
  - `clearProgramCacheOriginal (from ./parser)`
  - `clearWatchCaches (from ./create-program/getWatchProgramsForProjects)`
  - `clearTSConfigMatchCache (from ./parseSettings/createParseSettings)`
  - `clearTSServerProjectService (from ./parseSettings/createParseSettings)`
  - `clearGlobCache (from ./parseSettings/resolveProjectList)`

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