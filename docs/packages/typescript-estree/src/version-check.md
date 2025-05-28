[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `version-check.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/version-check.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `versions` | `readonly ["4.7", "4.8", "4.9", "5.0", "5.1", "5.2", "5.3", "5.4"]` | const | `[
  '4.7',
  '4.8',
  '4.9',
  '5.0',
  '5.1',
  '5.2',
  '5.3',
  '5.4',
] as const` | ✗ |
| `typescriptVersionIsAtLeast` | `Record<"4.7" | "4.8" | "4.9" | "5.0" | "5.1" | "5.2" | "5.3" | "5.4", boolean>` | const | `{} as Record<Versions, boolean>` | ✓ |


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

## Type Aliases

### `Versions`

```ts
type Versions = typeof versions extends ArrayLike<infer U> ? U : never;
```


---