[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `resolveProjectList.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/resolveProjectList.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `globSync` | `fast-glob` |
| `isGlob` | `is-glob` |
| `CanonicalPath` | `../create-program/shared` |
| `TSESTreeOptions` | `../parser-options` |
| `createHash` | `../create-program/shared` |
| `ensureAbsolutePath` | `../create-program/shared` |
| `getCanonicalFileName` | `../create-program/shared` |
| `DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS` | `./ExpiringCache` |
| `ExpiringCache` | `./ExpiringCache` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `RESOLUTION_CACHE` | `ExpiringCache<
  string,
  ReadonlyMap<CanonicalPath, string>
> | null` | let/var | `null` | ✗ |
| `sanitizedProjects` | `string[]` | const | `[]` | ✗ |
| `globProjectPaths` | `string[]` | let/var | `[]` | ✗ |
| `uniqueCanonicalProjectPaths` | `Map<CanonicalPath, string>` | const | `new Map(
    [...nonGlobProjects, ...globProjectPaths].map(project => [
      getCanonicalFileName(
        ensureAbsolutePath(project, options.tsconfigRootDir),
      ),
      ensureAbsolutePath(project, options.tsconfigRootDir),
    ]),
  )` | ✗ |
| `hashObject` | `{ tsconfigRootDir: string; project: readonly string[]; projectFolderIgnoreList: string[]; }` | const | `{
    tsconfigRootDir,
    // the project order does matter and can impact the resolved globs
    project,
    // the ignore order won't doesn't ever matter
    projectFolderIgnoreList: [...projectFolderIgnoreList].sort(),
  }` | ✗ |


---

## Functions

### `clearGlobCache(): void`

<details><summary>Code</summary>

```ts
export function clearGlobCache(): void {
  RESOLUTION_CACHE?.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `RESOLUTION_CACHE?.clear`
### `resolveProjectList(options: Readonly<{
    cacheLifetime?: TSESTreeOptions['cacheLifetime'];
    project: string[] | null;
    projectFolderIgnoreList: TSESTreeOptions['projectFolderIgnoreList'];
    singleRun: boolean;
    tsconfigRootDir: string;
  }>): ReadonlyMap<CanonicalPath, string>`

<details><summary>Code</summary>

```ts
export function resolveProjectList(
  options: Readonly<{
    cacheLifetime?: TSESTreeOptions['cacheLifetime'];
    project: string[] | null;
    projectFolderIgnoreList: TSESTreeOptions['projectFolderIgnoreList'];
    singleRun: boolean;
    tsconfigRootDir: string;
  }>,
): ReadonlyMap<CanonicalPath, string> {
  const sanitizedProjects: string[] = [];

  // Normalize and sanitize the project paths
  if (options.project != null) {
    for (const project of options.project) {
      if (typeof project === 'string') {
        sanitizedProjects.push(project);
      }
    }
  }

  if (sanitizedProjects.length === 0) {
    return new Map();
  }

  const projectFolderIgnoreList = (
    options.projectFolderIgnoreList ?? ['**/node_modules/**']
  )
    .filter(folder => typeof folder === 'string')
    // prefix with a ! for not match glob
    .map(folder => (folder.startsWith('!') ? folder : `!${folder}`));

  const cacheKey = getHash({
    project: sanitizedProjects,
    projectFolderIgnoreList,
    tsconfigRootDir: options.tsconfigRootDir,
  });
  if (RESOLUTION_CACHE == null) {
    // note - we initialize the global cache based on the first config we encounter.
    //        this does mean that you can't have multiple lifetimes set per folder
    //        I doubt that anyone will really bother reconfiguring this, let alone
    //        try to do complicated setups, so we'll deal with this later if ever.
    RESOLUTION_CACHE = new ExpiringCache(
      options.singleRun
        ? 'Infinity'
        : (options.cacheLifetime?.glob ??
          DEFAULT_TSCONFIG_CACHE_DURATION_SECONDS),
    );
  } else {
    const cached = RESOLUTION_CACHE.get(cacheKey);
    if (cached) {
      return cached;
    }
  }

  // Transform glob patterns into paths
  const nonGlobProjects = sanitizedProjects.filter(project => !isGlob(project));
  const globProjects = sanitizedProjects.filter(project => isGlob(project));

  let globProjectPaths: string[] = [];

  if (globProjects.length > 0) {
    // Although fast-glob supports multiple patterns, fast-glob returns arbitrary order of results
    // to improve performance. To ensure the order is correct, we need to call fast-glob for each pattern
    // separately and then concatenate the results in patterns' order.
    globProjectPaths = globProjects.flatMap(pattern =>
      globSync(pattern, {
        cwd: options.tsconfigRootDir,
        ignore: projectFolderIgnoreList,
      }),
    );
  }

  const uniqueCanonicalProjectPaths = new Map(
    [...nonGlobProjects, ...globProjectPaths].map(project => [
      getCanonicalFileName(
        ensureAbsolutePath(project, options.tsconfigRootDir),
      ),
      ensureAbsolutePath(project, options.tsconfigRootDir),
    ]),
  );

  log(
    'parserOptions.project (excluding ignored) matched projects: %s',
    uniqueCanonicalProjectPaths,
  );

  RESOLUTION_CACHE.set(cacheKey, uniqueCanonicalProjectPaths);
  return uniqueCanonicalProjectPaths;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Normalizes, sanitizes, resolves and filters the provided project paths
 */
```

- **Parameters**:
  - `options: Readonly<{
    cacheLifetime?: TSESTreeOptions['cacheLifetime'];
    project: string[] | null;
    projectFolderIgnoreList: TSESTreeOptions['projectFolderIgnoreList'];
    singleRun: boolean;
    tsconfigRootDir: string;
  }>`
- **Return Type**: `ReadonlyMap<CanonicalPath, string>`
- **Calls**:
  - `sanitizedProjects.push`
  - `(
    options.projectFolderIgnoreList ?? ['**/node_modules/**']
  )
    .filter(folder => typeof folder === 'string')
    // prefix with a ! for not match glob
    .map`
  - `folder.startsWith`
  - `getHash`
  - `RESOLUTION_CACHE.get`
  - `sanitizedProjects.filter`
  - `isGlob (from is-glob)`
  - `globProjects.flatMap`
  - `globSync (from fast-glob)`
  - `[...nonGlobProjects, ...globProjectPaths].map`
  - `getCanonicalFileName (from ../create-program/shared)`
  - `ensureAbsolutePath (from ../create-program/shared)`
  - `log`
  - `RESOLUTION_CACHE.set`
- **Internal Comments**:
```
// Normalize and sanitize the project paths
// note - we initialize the global cache based on the first config we encounter. (x3)
//        this does mean that you can't have multiple lifetimes set per folder (x3)
//        I doubt that anyone will really bother reconfiguring this, let alone (x3)
//        try to do complicated setups, so we'll deal with this later if ever. (x3)
// Transform glob patterns into paths (x2)
// Although fast-glob supports multiple patterns, fast-glob returns arbitrary order of results (x3)
// to improve performance. To ensure the order is correct, we need to call fast-glob for each pattern (x3)
// separately and then concatenate the results in patterns' order. (x3)
```

### `getHash({
  project,
  projectFolderIgnoreList,
  tsconfigRootDir,
}: Readonly<{
  project: readonly string[];
  projectFolderIgnoreList: readonly string[];
  tsconfigRootDir: string;
}>): string`

<details><summary>Code</summary>

```ts
function getHash({
  project,
  projectFolderIgnoreList,
  tsconfigRootDir,
}: Readonly<{
  project: readonly string[];
  projectFolderIgnoreList: readonly string[];
  tsconfigRootDir: string;
}>): string {
  // create a stable representation of the config
  const hashObject = {
    tsconfigRootDir,
    // the project order does matter and can impact the resolved globs
    project,
    // the ignore order won't doesn't ever matter
    projectFolderIgnoreList: [...projectFolderIgnoreList].sort(),
  };

  return createHash(JSON.stringify(hashObject));
}
```
</details>

- **Parameters**:
  - `{
  project,
  projectFolderIgnoreList,
  tsconfigRootDir,
}: Readonly<{
  project: readonly string[];
  projectFolderIgnoreList: readonly string[];
  tsconfigRootDir: string;
}>`
- **Return Type**: `string`
- **Calls**:
  - `[...projectFolderIgnoreList].sort`
  - `createHash (from ../create-program/shared)`
  - `JSON.stringify`
- **Internal Comments**:
```
// create a stable representation of the config (x2)
// the project order does matter and can impact the resolved globs (x2)
// the ignore order won't doesn't ever matter (x2)
```

### `clearGlobResolutionCache(): void`

<details><summary>Code</summary>

```ts
export function clearGlobResolutionCache(): void {
  RESOLUTION_CACHE?.clear();
  RESOLUTION_CACHE = null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Exported for testing purposes only
 * @internal
 */
```

- **Return Type**: `void`
- **Calls**:
  - `RESOLUTION_CACHE?.clear`

---