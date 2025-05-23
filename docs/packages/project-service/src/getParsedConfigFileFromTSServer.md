[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getParsedConfigFileFromTSServer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---