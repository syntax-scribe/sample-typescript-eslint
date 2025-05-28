[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `path.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 12 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 15 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website-eslint/src/mock/path.js`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `up` | `number` | let/var | `0` | ✗ |
| `last` | `any` | let/var | `parts[i]` | ✗ |
| `splitPathRe` | `RegExp` | let/var | `/^(\/?)([\s\S]*?)((?:\.{1,2}|[^/]+?)?(\.[^./]*|))\/*$/` | ✗ |
| `resolvedPath` | `string` | let/var | `''` | ✗ |
| `resolvedAbsolute` | `boolean` | let/var | `false` | ✗ |
| `path` | `any` | let/var | `i >= 0 ? args[i] : '/'` | ✗ |
| `start` | `number` | let/var | `0` | ✗ |
| `end` | `number` | let/var | `arr.length - 1` | ✗ |
| `samePartsLength` | `number` | let/var | `length` | ✗ |
| `sep` | `"/"` | let/var | `'/'` | ✓ |
| `delimiter` | `":"` | let/var | `':'` | ✓ |
| `root` | `string` | let/var | `result[0]` | ✗ |
| `dir` | `string` | let/var | `result[1]` | ✗ |
| `f` | `string` | let/var | `splitPath(path)[2]` | ✗ |
| `res` | `any[]` | let/var | `[]` | ✗ |


---

## Functions

### `normalizeArray(parts: any, allowAboveRoot: any): any`

<details><summary>Code</summary>

```ts
function normalizeArray(parts, allowAboveRoot) {
  // if the path tries to go above the root, `up` ends up > 0
  let up = 0;
  for (let i = parts.length - 1; i >= 0; i--) {
    const last = parts[i];
    if (last === '.') {
      parts.splice(i, 1);
    } else if (last === '..') {
      parts.splice(i, 1);
      up++;
    } else if (up) {
      parts.splice(i, 1);
      up--;
    }
  }

  // if the path is allowed to go above the root, restore leading ..s
  if (allowAboveRoot) {
    for (; up--; up) {
      parts.unshift('..');
    }
  }

  return parts;
}
```
</details>

- **Parameters**:
  - `parts: any`
  - `allowAboveRoot: any`
- **Return Type**: `any`
- **Calls**:
  - `parts.splice`
  - `parts.unshift`
- **Internal Comments**:
```
// if the path tries to go above the root, `up` ends up > 0 (x2)
// if the path is allowed to go above the root, restore leading ..s
```

### `splitPath(filename: any): string[]`

<details><summary>Code</summary>

```ts
function (filename) {
  return splitPathRe.exec(filename).slice(1);
}
```
</details>

- **Parameters**:
  - `filename: any`
- **Return Type**: `string[]`
- **Calls**:
  - `splitPathRe.exec(filename).slice`
### `resolve(args: any[]): string`

<details><summary>Code</summary>

```ts
export function resolve(...args) {
  let resolvedPath = '';
  let resolvedAbsolute = false;

  for (let i = args.length - 1; i >= -1 && !resolvedAbsolute; i--) {
    const path = i >= 0 ? args[i] : '/';

    // Skip empty and invalid entries
    if (typeof path !== 'string') {
      throw new TypeError('Arguments to path.resolve must be strings');
    } else if (!path) {
      continue;
    }

    resolvedPath = `${path}/${resolvedPath}`;
    resolvedAbsolute = path.charAt(0) === '/';
  }

  // At this point the path should be resolved to a full absolute path, but
  // handle relative paths to be safe (might happen when process.cwd() fails)

  // Normalize the path
  resolvedPath = normalizeArray(
    filter(resolvedPath.split('/'), p => !!p),
    !resolvedAbsolute,
  ).join('/');

  return (resolvedAbsolute ? '/' : '') + resolvedPath || '.';
}
```
</details>

- **Parameters**:
  - `args: any[]`
- **Return Type**: `string`
- **Calls**:
  - `path.charAt`
  - `normalizeArray(
    filter(resolvedPath.split('/'), p => !!p),
    !resolvedAbsolute,
  ).join`
- **Internal Comments**:
```
// Skip empty and invalid entries
// At this point the path should be resolved to a full absolute path, but (x3)
// handle relative paths to be safe (might happen when process.cwd() fails) (x3)
// Normalize the path (x3)
```

### `normalize(path: any): string`

<details><summary>Code</summary>

```ts
export function normalize(path) {
  const isPathAbsolute = isAbsolute(path);
  const trailingSlash = path.endsWith('/');

  // Normalize the path
  path = normalizeArray(
    filter(path.split('/'), p => !!p),
    !isPathAbsolute,
  ).join('/');

  if (!path && !isPathAbsolute) {
    path = '.';
  }
  if (path && trailingSlash) {
    path += '/';
  }

  return (isPathAbsolute ? '/' : '') + path;
}
```
</details>

- **Parameters**:
  - `path: any`
- **Return Type**: `string`
- **Calls**:
  - `isAbsolute`
  - `path.endsWith`
  - `normalizeArray(
    filter(path.split('/'), p => !!p),
    !isPathAbsolute,
  ).join`
- **Internal Comments**:
```
// Normalize the path (x3)
```

### `isAbsolute(path: any): boolean`

<details><summary>Code</summary>

```ts
export function isAbsolute(path) {
  return path.charAt(0) === '/';
}
```
</details>

- **Parameters**:
  - `path: any`
- **Return Type**: `boolean`
- **Calls**:
  - `path.charAt`
### `join(paths: any[]): string`

<details><summary>Code</summary>

```ts
export function join(...paths) {
  return normalize(
    filter(paths, p => {
      if (typeof p !== 'string') {
        throw new TypeError('Arguments to path.join must be strings');
      }
      return p;
    }).join('/'),
  );
}
```
</details>

- **Parameters**:
  - `paths: any[]`
- **Return Type**: `string`
- **Calls**:
  - `normalize`
  - `filter(paths, p => {
      if (typeof p !== 'string') {
        throw new TypeError('Arguments to path.join must be strings');
      }
      return p;
    }).join`
### `relative(from: any, to: any): string`

<details><summary>Code</summary>

```ts
export function relative(from, to) {
  from = resolve(from).slice(1);
  to = resolve(to).slice(1);

  function trim(arr) {
    let start = 0;
    for (; start < arr.length; start++) {
      if (arr[start] !== '') {
        break;
      }
    }

    let end = arr.length - 1;
    for (; end >= 0; end--) {
      if (arr[end] !== '') {
        break;
      }
    }

    if (start > end) {
      return [];
    }
    return arr.slice(start, end - start + 1);
  }

  const fromParts = trim(from.split('/'));
  const toParts = trim(to.split('/'));

  const length = Math.min(fromParts.length, toParts.length);
  let samePartsLength = length;
  for (let i = 0; i < length; i++) {
    if (fromParts[i] !== toParts[i]) {
      samePartsLength = i;
      break;
    }
  }

  return [
    ...Array(fromParts.length - samePartsLength).fill('..'),
    ...toParts.slice(samePartsLength),
  ].join('/');
}
```
</details>

- **Parameters**:
  - `from: any`
  - `to: any`
- **Return Type**: `string`
- **Calls**:
  - `resolve(from).slice`
  - `resolve(to).slice`
  - `arr.slice`
  - `trim`
  - `from.split`
  - `to.split`
  - `Math.min`
  - `[
    ...Array(fromParts.length - samePartsLength).fill('..'),
    ...toParts.slice(samePartsLength),
  ].join`
  - `Array(fromParts.length - samePartsLength).fill`
  - `toParts.slice`
### `trim(arr: any): any`

<details><summary>Code</summary>

```ts
function trim(arr) {
    let start = 0;
    for (; start < arr.length; start++) {
      if (arr[start] !== '') {
        break;
      }
    }

    let end = arr.length - 1;
    for (; end >= 0; end--) {
      if (arr[end] !== '') {
        break;
      }
    }

    if (start > end) {
      return [];
    }
    return arr.slice(start, end - start + 1);
  }
```
</details>

- **Parameters**:
  - `arr: any`
- **Return Type**: `any`
- **Calls**:
  - `arr.slice`
### `dirname(path: any): string`

<details><summary>Code</summary>

```ts
export function dirname(path) {
  const result = splitPath(path);
  const root = result[0];
  let dir = result[1];

  if (!root && !dir) {
    // No dirname whatsoever
    return '.';
  }

  if (dir) {
    // It has a dirname, strip trailing slash
    dir = dir.slice(0, -1);
  }

  return root + dir;
}
```
</details>

- **Parameters**:
  - `path: any`
- **Return Type**: `string`
- **Calls**:
  - `splitPath`
  - `dir.slice`
- **Internal Comments**:
```
// No dirname whatsoever
// It has a dirname, strip trailing slash (x3)
```

### `basename(path: any, ext: any): string`

<details><summary>Code</summary>

```ts
export function basename(path, ext) {
  let f = splitPath(path)[2];
  // TODO: make this comparison case-insensitive on windows?
  if (ext && f.slice(-1 * ext.length) === ext) {
    f = f.slice(0, f.length - ext.length);
  }
  return f;
}
```
</details>

- **Parameters**:
  - `path: any`
  - `ext: any`
- **Return Type**: `string`
- **Calls**:
  - `splitPath`
  - `f.slice`
- **Internal Comments**:
```
// TODO: make this comparison case-insensitive on windows?
```

### `extname(path: any): string`

<details><summary>Code</summary>

```ts
export function extname(path) {
  return splitPath(path)[3];
}
```
</details>

- **Parameters**:
  - `path: any`
- **Return Type**: `string`
- **Calls**:
  - `splitPath`
### `filter(xs: any, f: any): any`

<details><summary>Code</summary>

```ts
function filter(xs, f) {
  if (xs.filter) {
    return xs.filter(f);
  }
  const res = [];
  for (let i = 0; i < xs.length; i++) {
    if (f(xs[i], i, xs)) {
      res.push(xs[i]);
    }
  }
  return res;
}
```
</details>

- **Parameters**:
  - `xs: any`
  - `f: any`
- **Return Type**: `any`
- **Calls**:
  - `xs.filter`
  - `f`
  - `res.push`

---