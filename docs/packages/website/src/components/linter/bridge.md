[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `bridge.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/bridge.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ConfigModel` | `../types` |
| `PlaygroundSystem` | `./types` |
| `debounce` | `../lib/debounce` |
| `getPathRegExp` | `./utils` |


---

## Functions

### `createFileSystem(config: Pick<ConfigModel, 'code' | 'eslintrc' | 'fileType' | 'tsconfig'>, vfs: typeof tsvfs): PlaygroundSystem`

<details><summary>Code</summary>

```ts
export function createFileSystem(
  config: Pick<ConfigModel, 'code' | 'eslintrc' | 'fileType' | 'tsconfig'>,
  vfs: typeof tsvfs,
): PlaygroundSystem {
  const files = new Map<string, string>();
  files.set(`/.eslintrc`, config.eslintrc);
  files.set(`/tsconfig.json`, config.tsconfig);
  files.set(`/input${config.fileType}`, config.code);

  const fileWatcherCallbacks = new Map<RegExp, Set<ts.FileWatcherCallback>>();

  const system = vfs.createSystem(files) as PlaygroundSystem;

  system.watchFile = (
    path,
    callback,
    pollingInterval = 500,
  ): ts.FileWatcher => {
    const cb = pollingInterval ? debounce(callback, pollingInterval) : callback;
    const expPath = getPathRegExp(path);
    let handle = fileWatcherCallbacks.get(expPath);
    if (!handle) {
      handle = new Set();
      fileWatcherCallbacks.set(expPath, handle);
    }
    handle.add(cb);

    return {
      close: (): void => {
        fileWatcherCallbacks.get(expPath)?.delete(cb);
      },
    };
  };

  const triggerCallbacks = (
    path: string,
    type: ts.FileWatcherEventKind,
  ): void => {
    fileWatcherCallbacks.forEach((callbacks, key) => {
      if (key.test(path)) {
        callbacks.forEach(cb => cb(path, type));
      }
    });
  };

  system.deleteFile = (fileName): void => {
    files.delete(fileName);
    triggerCallbacks(fileName, 1);
  };

  system.writeFile = (fileName, contents): void => {
    if (!contents) {
      contents = '';
    }
    const file = files.get(fileName);
    if (file === contents) {
      // do not trigger callbacks if the file has not changed
      return;
    }
    files.set(fileName, contents);
    triggerCallbacks(fileName, file ? 2 : 0);
  };

  system.removeFile = (fileName): void => {
    files.delete(fileName);
  };

  system.searchFiles = (path: string): string[] => {
    const expPath = getPathRegExp(path);
    return [...files.keys()].filter(fileName => expPath.test(fileName));
  };

  return system;
}
```
</details>

- **Parameters**:
  - `config: Pick<ConfigModel, 'code' | 'eslintrc' | 'fileType' | 'tsconfig'>`
  - `vfs: typeof tsvfs`
- **Return Type**: `PlaygroundSystem`
- **Calls**:
  - `files.set`
  - `vfs.createSystem`
  - `debounce (from ../lib/debounce)`
  - `getPathRegExp (from ./utils)`
  - `fileWatcherCallbacks.get`
  - `fileWatcherCallbacks.set`
  - `handle.add`
  - `fileWatcherCallbacks.get(expPath)?.delete`
  - `fileWatcherCallbacks.forEach`
  - `key.test`
  - `callbacks.forEach`
  - `cb`
  - `files.delete`
  - `triggerCallbacks`
  - `files.get`
  - `[...files.keys()].filter`
  - `files.keys`
  - `expPath.test`
- **Internal Comments**:
```
// do not trigger callbacks if the file has not changed
```

### `close(): void`

<details><summary>Code</summary>

```ts
(): void => {
        fileWatcherCallbacks.get(expPath)?.delete(cb);
      }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `fileWatcherCallbacks.get(expPath)?.delete`
### `close(): void`

<details><summary>Code</summary>

```ts
(): void => {
        fileWatcherCallbacks.get(expPath)?.delete(cb);
      }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `fileWatcherCallbacks.get(expPath)?.delete`
### `triggerCallbacks(path: string, type: ts.FileWatcherEventKind): void`

<details><summary>Code</summary>

```ts
(
    path: string,
    type: ts.FileWatcherEventKind,
  ): void => {
    fileWatcherCallbacks.forEach((callbacks, key) => {
      if (key.test(path)) {
        callbacks.forEach(cb => cb(path, type));
      }
    });
  }
```
</details>

- **Parameters**:
  - `path: string`
  - `type: ts.FileWatcherEventKind`
- **Return Type**: `void`
- **Calls**:
  - `fileWatcherCallbacks.forEach`
  - `key.test`
  - `callbacks.forEach`
  - `cb`

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