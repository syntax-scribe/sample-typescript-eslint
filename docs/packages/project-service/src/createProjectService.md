[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `createProjectService.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 47 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 6 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/project-service/src/createProjectService.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ProjectServiceOptions` | `@typescript-eslint/types` |
| `debug` | `debug` |
| `getParsedConfigFileFromTSServer` | `./getParsedConfigFileFromTSServer.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PROJECT_MATCHED_FILES_THRESHOLD` | `8` | const | `8` | ✗ |
| `options` | `any` | const | `{
    defaultProject: 'tsconfig.json',
    ...optionsRaw,
  }` | ✗ |
| `tsserver` | `any` | const | `require('typescript/lib/tsserverlibrary') as typeof ts` | ✗ |
| `system` | `ts.server.ServerHost` | const | `{
    ...tsserver.sys,
    clearImmediate,
    clearTimeout,
    setImmediate,
    setTimeout,
    watchDirectory: createStubFileWatcher,
    watchFile: createStubFileWatcher,

    // We stop loading any TypeScript plugins by default, to prevent them from attaching disk watchers
    // See https://github.com/typescript-eslint/typescript-eslint/issues/9905
    ...(!options.loadTypeScriptPlugins && {
      require: () => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      }),
    }),
  }` | ✗ |
| `logger` | `ts.server.Logger` | const | `{
    close: doNothing,
    endGroup: doNothing,
    getLogFileName: (): undefined => undefined,
    // The debug library doesn't use levels without creating a namespace for each.
    // Log levels are not passed to the writer so we wouldn't be able to forward
    // to a respective namespace.  Supporting would require an additional flag for
    // granular control.  Defaulting to all levels for now.
    hasLevel: (): boolean => true,
    info(s) {
      this.msg(s, tsserver.server.Msg.Info);
    },
    loggingEnabled: (): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled,
    msg: (s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    },
    perftrc(s) {
      this.msg(s, tsserver.server.Msg.Perf);
    },
    startGroup: doNothing,
  }` | ✗ |
| `service` | `any` | const | `new tsserver.server.ProjectService({
    cancellationToken: { isCancellationRequested: (): boolean => false },
    eventHandler: logTsserverEvent.enabled
      ? (e): void => {
          logTsserverEvent(e);
        }
      : undefined,
    host: system,
    jsDocParsingMode,
    logger,
    session: undefined,
    useInferredProjectPerProjectRoot: false,
    useSingleInferredProject: false,
  })` | ✗ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `@typescript-eslint/types` | ProjectServiceOptions |


---

## Functions

### `doNothing(): void`

<details><summary>Code</summary>

```ts
(): void => {}
```
</details>

- **Return Type**: `void`
### `createStubFileWatcher(): ts.FileWatcher`

<details><summary>Code</summary>

```ts
(): ts.FileWatcher => ({
  close: doNothing,
})
```
</details>

- **Return Type**: `ts.FileWatcher`
### `createProjectService({
  jsDocParsingMode,
  options: optionsRaw = {},
  tsconfigRootDir,
}: CreateProjectServiceSettings): ProjectServiceAndMetadata`

<details><summary>Code</summary>

```ts
export function createProjectService({
  jsDocParsingMode,
  options: optionsRaw = {},
  tsconfigRootDir,
}: CreateProjectServiceSettings = {}): ProjectServiceAndMetadata {
  const options = {
    defaultProject: 'tsconfig.json',
    ...optionsRaw,
  };

  // We import this lazily to avoid its cost for users who don't use the service
  // TODO: Once we drop support for TS<5.3 we can import from "typescript" directly
  // eslint-disable-next-line @typescript-eslint/no-require-imports
  const tsserver = require('typescript/lib/tsserverlibrary') as typeof ts;

  // TODO: see getWatchProgramsForProjects
  // We don't watch the disk, we just refer to these when ESLint calls us
  // there's a whole separate update pass in maybeInvalidateProgram at the bottom of getWatchProgramsForProjects
  // (this "goes nuclear on TypeScript")
  const system: ts.server.ServerHost = {
    ...tsserver.sys,
    clearImmediate,
    clearTimeout,
    setImmediate,
    setTimeout,
    watchDirectory: createStubFileWatcher,
    watchFile: createStubFileWatcher,

    // We stop loading any TypeScript plugins by default, to prevent them from attaching disk watchers
    // See https://github.com/typescript-eslint/typescript-eslint/issues/9905
    ...(!options.loadTypeScriptPlugins && {
      require: () => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      }),
    }),
  };

  const logger: ts.server.Logger = {
    close: doNothing,
    endGroup: doNothing,
    getLogFileName: (): undefined => undefined,
    // The debug library doesn't use levels without creating a namespace for each.
    // Log levels are not passed to the writer so we wouldn't be able to forward
    // to a respective namespace.  Supporting would require an additional flag for
    // granular control.  Defaulting to all levels for now.
    hasLevel: (): boolean => true,
    info(s) {
      this.msg(s, tsserver.server.Msg.Info);
    },
    loggingEnabled: (): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled,
    msg: (s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    },
    perftrc(s) {
      this.msg(s, tsserver.server.Msg.Perf);
    },
    startGroup: doNothing,
  };

  log('Creating Project Service with: %o', options);

  const service = new tsserver.server.ProjectService({
    cancellationToken: { isCancellationRequested: (): boolean => false },
    eventHandler: logTsserverEvent.enabled
      ? (e): void => {
          logTsserverEvent(e);
        }
      : undefined,
    host: system,
    jsDocParsingMode,
    logger,
    session: undefined,
    useInferredProjectPerProjectRoot: false,
    useSingleInferredProject: false,
  });

  service.setHostConfiguration({
    preferences: {
      includePackageJsonAutoImports: 'off',
    },
  });

  log('Enabling default project: %s', options.defaultProject);

  const configFile = getParsedConfigFileFromTSServer(
    tsserver,
    options.defaultProject,
    !!optionsRaw.defaultProject,
    tsconfigRootDir,
  );

  if (configFile) {
    service.setCompilerOptionsForInferredProjects(
      // NOTE: The inferred projects API is not intended for source files when a tsconfig
      // exists. There is no API that generates an InferredProjectCompilerOptions suggesting
      // it is meant for hard coded options passed in. Hard asserting as a work around.
      // See https://github.com/microsoft/TypeScript/blob/27bcd4cb5a98bce46c9cdd749752703ead021a4b/src/server/protocol.ts#L1904
      configFile.options as ts.server.protocol.InferredProjectCompilerOptions,
    );
  }

  return {
    allowDefaultProject: options.allowDefaultProject,
    lastReloadTimestamp: performance.now(),
    maximumDefaultProjectFileMatchCount:
      options.maximumDefaultProjectFileMatchCount_THIS_WILL_SLOW_DOWN_LINTING ??
      DEFAULT_PROJECT_MATCHED_FILES_THRESHOLD,
    service,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Creates a new Project Service instance, as well as metadata on its creation.
 * @param settings Settings to create a new Project Service instance.
 * @returns A new Project Service instance, as well as metadata on its creation.
 * @example
 * ```ts
 * import { createProjectService } from '@typescript-eslint/project-service';
 *
 * const { service } = createProjectService();
 *
 * service.openClientFile('index.ts');
 * ```
 */
```

- **Parameters**:
  - `{
  jsDocParsingMode,
  options: optionsRaw = {},
  tsconfigRootDir,
}: CreateProjectServiceSettings`
- **Return Type**: `ProjectServiceAndMetadata`
- **Calls**:
  - `require`
  - `this.msg`
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
  - `log`
  - `logTsserverEvent`
  - `service.setHostConfiguration`
  - `getParsedConfigFileFromTSServer (from ./getParsedConfigFileFromTSServer.js)`
  - `service.setCompilerOptionsForInferredProjects`
  - `performance.now`
- **Internal Comments**:
```
// We import this lazily to avoid its cost for users who don't use the service (x2)
// TODO: Once we drop support for TS<5.3 we can import from "typescript" directly (x2)
// eslint-disable-next-line @typescript-eslint/no-require-imports (x2)
// TODO: see getWatchProgramsForProjects (x2)
// We don't watch the disk, we just refer to these when ESLint calls us (x2)
// there's a whole separate update pass in maybeInvalidateProgram at the bottom of getWatchProgramsForProjects (x2)
// (this "goes nuclear on TypeScript") (x2)
// We stop loading any TypeScript plugins by default, to prevent them from attaching disk watchers
// See https://github.com/typescript-eslint/typescript-eslint/issues/9905
// The debug library doesn't use levels without creating a namespace for each. (x2)
// Log levels are not passed to the writer so we wouldn't be able to forward (x2)
// to a respective namespace.  Supporting would require an additional flag for (x2)
// granular control.  Defaulting to all levels for now. (x2)
// if none of the debug namespaces are enabled, then don't enable logging in tsserver (x4)
// NOTE: The inferred projects API is not intended for source files when a tsconfig (x3)
// exists. There is no API that generates an InferredProjectCompilerOptions suggesting (x3)
// it is meant for hard coded options passed in. Hard asserting as a work around. (x3)
// See https://github.com/microsoft/TypeScript/blob/27bcd4cb5a98bce46c9cdd749752703ead021a4b/src/server/protocol.ts#L1904 (x3)
```

### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `require(): { error: { message: string; }; module: any; }`

<details><summary>Code</summary>

```ts
() => ({
        error: {
          message:
            'TypeScript plugins are not required when using parserOptions.projectService.',
        },
        module: undefined,
      })
```
</details>

- **Return Type**: `{ error: { message: string; }; module: any; }`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `getLogFileName(): undefined`

<details><summary>Code</summary>

```ts
(): undefined => undefined
```
</details>

- **Return Type**: `undefined`
### `hasLevel(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => true
```
</details>

- **Return Type**: `boolean`
### `loggingEnabled(): boolean`

<details><summary>Code</summary>

```ts
(): boolean =>
      // if none of the debug namespaces are enabled, then don't enable logging in tsserver
      logTsserverInfo.enabled ||
      logTsserverErr.enabled ||
      logTsserverPerf.enabled
```
</details>

- **Return Type**: `boolean`
- **Internal Comments**:
```
// if none of the debug namespaces are enabled, then don't enable logging in tsserver
```

### `msg(s: any, type: any): void`

<details><summary>Code</summary>

```ts
(s, type) => {
      switch (type) {
        case tsserver.server.Msg.Err:
          logTsserverErr(s);
          break;
        case tsserver.server.Msg.Perf:
          logTsserverPerf(s);
          break;
        default:
          logTsserverInfo(s);
      }
    }
```
</details>

- **Parameters**:
  - `s: any`
  - `type: any`
- **Return Type**: `void`
- **Calls**:
  - `logTsserverErr`
  - `logTsserverPerf`
  - `logTsserverInfo`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`
### `isCancellationRequested(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => false
```
</details>

- **Return Type**: `boolean`

---

## Interfaces

### `ProjectServiceAndMetadata`

<details><summary>Interface Code</summary>

```ts
export interface ProjectServiceAndMetadata {
  /**
   * Files allowed to be loaded from the default project, if any were specified.
   */
  allowDefaultProject: string[] | undefined;

  /**
   * The performance.now() timestamp of the last reload of the project service.
   */
  lastReloadTimestamp: number;

  /**
   * The maximum number of files that can be matched by the default project.
   */
  maximumDefaultProjectFileMatchCount: number;

  /**
   * The created TypeScript Project Service instance.
   */
  service: TypeScriptProjectService;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowDefaultProject` | `string[] | undefined` | ✗ |  |
| `lastReloadTimestamp` | `number` | ✗ |  |
| `maximumDefaultProjectFileMatchCount` | `number` | ✗ |  |
| `service` | `TypeScriptProjectService` | ✗ |  |

### `CreateProjectServiceSettings`

<details><summary>Interface Code</summary>

```ts
export interface CreateProjectServiceSettings {
  /**
   * Granular options to configure the project service.
   */
  options?: ProjectServiceOptions;

  /**
   * How aggressively (and slowly) to parse JSDoc comments.
   */
  jsDocParsingMode?: ts.JSDocParsingMode;

  /**
   * Root directory for the tsconfig.json file, if not the current directory.
   */
  tsconfigRootDir?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `options` | `ProjectServiceOptions` | ✓ |  |
| `jsDocParsingMode` | `ts.JSDocParsingMode` | ✓ |  |
| `tsconfigRootDir` | `string` | ✓ |  |


---

## Type Aliases

### `TypeScriptProjectService`

/**
 * Shortcut type to refer to TypeScript's server ProjectService.
 */

```ts
type TypeScriptProjectService = ts.server.ProjectService;
```


---