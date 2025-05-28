[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useProgramFromProjectService.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 38 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 13 |
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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `currentDirectory` | `"/repos/repo"` | const | `'/repos/repo'` | ✗ |
| `service` | `{ getDefaultProjectForFile: () => { getLanguageService: () => { getProgram: any; }; }; getScriptInfo: () => {}; host: { getCurrentDirectory: () => string; }; openClientFile: any; reloadProjects: any; setHostConfiguration: any; }` | const | `{
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
  }` | ✗ |
| `mockFileName` | `"camelCaseFile.ts"` | const | `'camelCaseFile.ts'` | ✗ |
| `mockParseSettings` | `Readonly<MutableParseSettings>` | const | `{
  extraFileExtensions: [] as readonly string[],
  filePath: `path/PascalCaseDirectory/${mockFileName}`,
  singleRun: false,
  tsconfigRootDir: currentDirectory,
} as ParseSettings` | ✗ |
| `stubASTAndNoProgram` | `{ ast: any; program: any; }` | const | `{
      ast: ts.createSourceFile(mockFileName, '', ts.ScriptTarget.Latest),
      program: null,
    }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `program` | `{ getSourceFile: any; }` | const | `{ getSourceFile: vi.fn() }` | ✗ |
| `filePath` | `"path/PascalCaseDirectory/vue-component.vue"` | const | ``path/PascalCaseDirectory/vue-component.vue`` | ✗ |
| `filePath` | `"path/PascalCaseDirectory/vue-component.vue"` | const | ``path/PascalCaseDirectory/vue-component.vue`` | ✗ |


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