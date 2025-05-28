[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getParsedConfigFileFromTSServer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 0 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/project-service/src/getParsedConfigFileFromTSServer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getParsedConfigFile` | `@typescript-eslint/tsconfig-utils` |


---

## Functions

### `getParsedConfigFileFromTSServer(tsserver: typeof ts, defaultProject: string, throwOnFailure: boolean, tsconfigRootDir: string): ts.ParsedCommandLine | undefined`

<details><summary>Code</summary>

```ts
export function getParsedConfigFileFromTSServer(
  tsserver: typeof ts,
  defaultProject: string,
  throwOnFailure: boolean,
  tsconfigRootDir?: string,
): ts.ParsedCommandLine | undefined {
  try {
    return getParsedConfigFile(tsserver, defaultProject, tsconfigRootDir);
  } catch (error) {
    if (throwOnFailure) {
      throw new Error(
        `Could not read Project Service default project '${defaultProject}': ${(error as Error).message}`,
      );
    }
  }

  return undefined;
}
```
</details>

- **Parameters**:
  - `tsserver: typeof ts`
  - `defaultProject: string`
  - `throwOnFailure: boolean`
  - `tsconfigRootDir: string`
- **Return Type**: `ts.ParsedCommandLine | undefined`
- **Calls**:
  - `getParsedConfigFile (from @typescript-eslint/tsconfig-utils)`

---