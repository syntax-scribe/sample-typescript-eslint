[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `clear-caches.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `clearProgramCache` | `() => void` | const | `clearCaches` | ✓ |


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