[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `test-utils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/test-utils/test-utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParseAndGenerateServicesResult` | `../../src` |
| `TSESTreeOptions` | `../../src` |
| `parseAndGenerateServices` | `../../src` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `node` | `{ [x: string]: unknown; }` | const | `{ ...oNode }` | ✗ |
| `child` | `UnknownObject | UnknownObject[]` | const | `node[prop] as UnknownObject | UnknownObject[]` | ✗ |
| `value` | `any[]` | const | `[]` | ✗ |


---

## Functions

### `parseCodeAndGenerateServices(code: string, config: TSESTreeOptions): ParseAndGenerateServicesResult<TSESTreeOptions>`

<details><summary>Code</summary>

```ts
export function parseCodeAndGenerateServices(
  code: string,
  config: TSESTreeOptions,
): ParseAndGenerateServicesResult<TSESTreeOptions> {
  return parseAndGenerateServices(code, config);
}
```
</details>

- **Parameters**:
  - `code: string`
  - `config: TSESTreeOptions`
- **Return Type**: `ParseAndGenerateServicesResult<TSESTreeOptions>`
- **Calls**:
  - `parseAndGenerateServices (from ../../src)`
### `formatSnapshotName(filename: string, fixturesDir: string, fileExtension: string): string`

<details><summary>Code</summary>

```ts
export function formatSnapshotName(
  filename: string,
  fixturesDir: string,
  fileExtension = '.js',
): string {
  return `fixtures/${filename
    .replace(`${fixturesDir}/`, '')
    .replace(fileExtension, '')}`;
}
```
</details>

- **Parameters**:
  - `filename: string`
  - `fixturesDir: string`
  - `fileExtension: string`
- **Return Type**: `string`
- **Calls**:
  - `filename
    .replace(`${fixturesDir}/`, '')
    .replace`
### `isJSXFileType(fileType: string): boolean`

<details><summary>Code</summary>

```ts
export function isJSXFileType(fileType: string): boolean {
  if (fileType.startsWith('.')) {
    fileType = fileType.slice(1);
  }
  return fileType === 'js' || fileType === 'jsx' || fileType === 'tsx';
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if file extension is one used for jsx
 */
```

- **Parameters**:
  - `fileType: string`
- **Return Type**: `boolean`
- **Calls**:
  - `fileType.startsWith`
  - `fileType.slice`
### `deeplyCopy(ast: T): T`

<details><summary>Code</summary>

```ts
export function deeplyCopy<T extends NonNullable<unknown>>(ast: T): T {
  return omitDeep(ast) as T;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns a raw copy of the typescript AST
 * @param ast the AST object
 * @returns copy of the AST object
 */
```

- **Parameters**:
  - `ast: T`
- **Return Type**: `T`
- **Calls**:
  - `omitDeep`
### `isObjectLike(value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isObjectLike(value: unknown): boolean {
  return (
    typeof value === 'object' && !(value instanceof RegExp) && value != null
  );
}
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `boolean`
### `omitDeep(root: UnknownObject, keysToOmit: { key: string; predicate: (value: unknown) => boolean }[], selectors: Record<
    string,
    (node: UnknownObject, parent: UnknownObject | null) => void
  >): UnknownObject`

<details><summary>Code</summary>

```ts
export function omitDeep(
  root: UnknownObject,
  keysToOmit: { key: string; predicate: (value: unknown) => boolean }[] = [],
  selectors: Record<
    string,
    (node: UnknownObject, parent: UnknownObject | null) => void
  > = {},
): UnknownObject {
  function shouldOmit(keyName: string, val: unknown): boolean {
    if (keysToOmit.length) {
      return keysToOmit.some(
        keyConfig => keyConfig.key === keyName && keyConfig.predicate(val),
      );
    }
    return false;
  }

  function visit(
    oNode: UnknownObject,
    parent: UnknownObject | null,
  ): UnknownObject {
    if (!Array.isArray(oNode) && !isObjectLike(oNode)) {
      return oNode;
    }

    const node = { ...oNode };

    for (const prop in node) {
      if (Object.hasOwn(node, prop)) {
        // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
        if (shouldOmit(prop, node[prop]) || node[prop] === undefined) {
          // Filter out omitted and undefined props from the node
          // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
          delete node[prop];
          continue;
        }

        const child = node[prop] as UnknownObject | UnknownObject[];
        if (Array.isArray(child)) {
          const value = [];
          for (const el of child) {
            value.push(visit(el, node));
          }
          node[prop] = value;
        } else if (isObjectLike(child)) {
          node[prop] = visit(child, node);
        }
      }
    }

    if (typeof node.type === 'string' && node.type in selectors) {
      selectors[node.type](node, parent);
    }

    return node;
  }

  return visit(root, null);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Removes the given keys from the given AST object recursively
 * @param root A JavaScript object to remove keys from
 * @param keysToOmit Names and predicate functions use to determine what keys to omit from the final object
 * @param selectors advance ast modifications
 * @returns formatted object
 */
```

- **Parameters**:
  - `root: UnknownObject`
  - `keysToOmit: { key: string; predicate: (value: unknown) => boolean }[]`
  - `selectors: Record<
    string,
    (node: UnknownObject, parent: UnknownObject | null) => void
  >`
- **Return Type**: `UnknownObject`
- **Calls**:
  - `keysToOmit.some`
  - `keyConfig.predicate`
  - `Array.isArray`
  - `isObjectLike`
  - `Object.hasOwn`
  - `shouldOmit`
  - `value.push`
  - `visit`
  - `complex_call_3100`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
// Filter out omitted and undefined props from the node (x2)
// eslint-disable-next-line @typescript-eslint/no-dynamic-delete (x2)
```

### `shouldOmit(keyName: string, val: unknown): boolean`

<details><summary>Code</summary>

```ts
function shouldOmit(keyName: string, val: unknown): boolean {
    if (keysToOmit.length) {
      return keysToOmit.some(
        keyConfig => keyConfig.key === keyName && keyConfig.predicate(val),
      );
    }
    return false;
  }
```
</details>

- **Parameters**:
  - `keyName: string`
  - `val: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `keysToOmit.some`
  - `keyConfig.predicate`
### `visit(oNode: UnknownObject, parent: UnknownObject | null): UnknownObject`

<details><summary>Code</summary>

```ts
function visit(
    oNode: UnknownObject,
    parent: UnknownObject | null,
  ): UnknownObject {
    if (!Array.isArray(oNode) && !isObjectLike(oNode)) {
      return oNode;
    }

    const node = { ...oNode };

    for (const prop in node) {
      if (Object.hasOwn(node, prop)) {
        // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
        if (shouldOmit(prop, node[prop]) || node[prop] === undefined) {
          // Filter out omitted and undefined props from the node
          // eslint-disable-next-line @typescript-eslint/no-dynamic-delete
          delete node[prop];
          continue;
        }

        const child = node[prop] as UnknownObject | UnknownObject[];
        if (Array.isArray(child)) {
          const value = [];
          for (const el of child) {
            value.push(visit(el, node));
          }
          node[prop] = value;
        } else if (isObjectLike(child)) {
          node[prop] = visit(child, node);
        }
      }
    }

    if (typeof node.type === 'string' && node.type in selectors) {
      selectors[node.type](node, parent);
    }

    return node;
  }
```
</details>

- **Parameters**:
  - `oNode: UnknownObject`
  - `parent: UnknownObject | null`
- **Return Type**: `UnknownObject`
- **Calls**:
  - `Array.isArray`
  - `isObjectLike`
  - `Object.hasOwn`
  - `shouldOmit`
  - `value.push`
  - `visit`
  - `complex_call_3100`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish
// Filter out omitted and undefined props from the node (x2)
// eslint-disable-next-line @typescript-eslint/no-dynamic-delete (x2)
```


---

## Type Aliases

### `UnknownObject`

```ts
type UnknownObject = Record<string, unknown>;
```


---