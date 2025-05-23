[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useProgramFromProjectService.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 20
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/lib/useProgramFromProjectService.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ProjectServiceAndMetadata` | `@typescript-eslint/project-service` |
| `TypeScriptProjectService` | `@typescript-eslint/project-service` |
| `path` | `node:path` |
| `ParseSettings` | `../../src/parseSettings` |
| `useProgramFromProjectService` | `../../src/useProgramFromProjectService` |


---

## Functions

### `createMockProjectService(): { openClientFile: any; reloadProjects: any; service: any; }`

<details><summary>Code</summary>

```ts
function createMockProjectService() {
  const openClientFile = vi.fn();
  const setHostConfiguration = vi.fn();
  const reloadProjects = vi.fn();
  const service = {
    getDefaultProjectForFile: () => ({
      getLanguageService: () => ({
        getProgram: mockGetProgram,
      }),
    }),
    getScriptInfo: () => ({}),
    host: {
      getCurrentDirectory: () => currentDirectory,
    },
    openClientFile,
    reloadProjects,
    setHostConfiguration,
  };

  return {
    openClientFile,
    reloadProjects,
    service: service as typeof service & TypeScriptProjectService,
  };
}
```
</details>

- **Return Type**: `{ openClientFile: any; reloadProjects: any; service: any; }`
- **Calls**:
  - `vi.fn`
### `getDefaultProjectForFile(): { getLanguageService: () => { getProgram: any; }; }`

<details><summary>Code</summary>

```ts
() => ({
      getLanguageService: () => ({
        getProgram: mockGetProgram,
      }),
    })
```
</details>

- **Return Type**: `{ getLanguageService: () => { getProgram: any; }; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getScriptInfo(): {}`

<details><summary>Code</summary>

```ts
() => ({})
```
</details>

- **Return Type**: `{}`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `getDefaultProjectForFile(): { getLanguageService: () => { getProgram: any; }; }`

<details><summary>Code</summary>

```ts
() => ({
      getLanguageService: () => ({
        getProgram: mockGetProgram,
      }),
    })
```
</details>

- **Return Type**: `{ getLanguageService: () => { getProgram: any; }; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getScriptInfo(): {}`

<details><summary>Code</summary>

```ts
() => ({})
```
</details>

- **Return Type**: `{}`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `getDefaultProjectForFile(): { getLanguageService: () => { getProgram: any; }; }`

<details><summary>Code</summary>

```ts
() => ({
      getLanguageService: () => ({
        getProgram: mockGetProgram,
      }),
    })
```
</details>

- **Return Type**: `{ getLanguageService: () => { getProgram: any; }; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getLanguageService(): { getProgram: any; }`

<details><summary>Code</summary>

```ts
() => ({
        getProgram: mockGetProgram,
      })
```
</details>

- **Return Type**: `{ getProgram: any; }`
### `getScriptInfo(): {}`

<details><summary>Code</summary>

```ts
() => ({})
```
</details>

- **Return Type**: `{}`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `getCurrentDirectory(): string`

<details><summary>Code</summary>

```ts
() => currentDirectory
```
</details>

- **Return Type**: `string`
### `createProjectServiceSettings(settings: T): { lastReloadTimestamp: number; maximumDefaultProjectFileMatchCount: number; } & T`

<details><summary>Code</summary>

```ts
<
  T extends Partial<ProjectServiceAndMetadata>,
>(
  settings: T,
) => ({
  lastReloadTimestamp: 0,
  maximumDefaultProjectFileMatchCount: 8,
  ...settings,
})
```
</details>

- **Parameters**:
  - `settings: T`
- **Return Type**: `{ lastReloadTimestamp: number; maximumDefaultProjectFileMatchCount: number; } & T`

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