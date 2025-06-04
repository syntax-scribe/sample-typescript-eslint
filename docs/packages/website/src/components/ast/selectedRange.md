[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `selectedRange.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/selectedRange.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParentNodeType` | `./types` |
| `filterProperties` | `./utils` |
| `isESNode` | `./utils` |
| `isRecord` | `./utils` |
| `isTSNode` | `./utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `arrayChild` | `unknown` | const | `child[index]` | ✗ |
| `nodePath` | `string[]` | const | `['ast']` | ✗ |
| `visited` | `Set<unknown>` | const | `new Set<unknown>()` | ✗ |
| `currentNode` | `unknown` | let/var | `node` | ✗ |


---

## Functions

### `isInRange(offset: number, value: object): boolean`

<details><summary>Code</summary>

```ts
function isInRange(offset: number, value: object): boolean {
  const range = getRangeFromNode(value);
  return !!range && offset > range[0] && offset <= range[1];
}
```
</details>

- **Parameters**:
  - `offset: number`
  - `value: object`
- **Return Type**: `boolean`
- **Calls**:
  - `getRangeFromNode`
### `geNodeType(value: unknown): ParentNodeType`

<details><summary>Code</summary>

```ts
function geNodeType(value: unknown): ParentNodeType {
  if (isRecord(value)) {
    return isESNode(value) ? 'esNode' : isTSNode(value) ? 'tsNode' : undefined;
  }
  return undefined;
}
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `ParentNodeType`
- **Calls**:
  - `isRecord (from ./utils)`
  - `isESNode (from ./utils)`
  - `isTSNode (from ./utils)`
### `isIterable(key: string, value: unknown): boolean`

<details><summary>Code</summary>

```ts
function isIterable(key: string, value: unknown): boolean {
  return filterProperties(key, value, geNodeType(value));
}
```
</details>

- **Parameters**:
  - `key: string`
  - `value: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `filterProperties (from ./utils)`
  - `geNodeType`
### `getRangeFromNode(value: object): [number, number] | null`

<details><summary>Code</summary>

```ts
function getRangeFromNode(value: object): [number, number] | null {
  if (isESNode(value)) {
    return value.range;
  }
  if (isTSNode(value)) {
    return [value.pos, value.end];
  }
  return null;
}
```
</details>

- **Parameters**:
  - `value: object`
- **Return Type**: `[number, number] | null`
- **Calls**:
  - `isESNode (from ./utils)`
  - `isTSNode (from ./utils)`
### `findInObject(iter: object, cursorPosition: number, visited: Set<unknown>): {
  key: string[];
  value: unknown;
} | null`

<details><summary>Code</summary>

```ts
function findInObject(
  iter: object,
  cursorPosition: number,
  visited: Set<unknown>,
): {
  key: string[];
  value: unknown;
} | null {
  const children = Object.entries(iter);
  for (const [name, child] of children) {
    // we do not want to select parents in case if we do filter with esquery
    if (visited.has(child) || name === 'parent' || !isIterable(name, child)) {
      continue;
    }
    visited.add(iter);

    if (isRecord(child)) {
      if (isInRange(cursorPosition, child)) {
        return {
          key: [name],
          value: child,
        };
      }
    } else if (Array.isArray(child)) {
      for (let index = 0; index < child.length; ++index) {
        const arrayChild: unknown = child[index];
        // typescript array like elements have other iterable items
        if (
          typeof index === 'number' &&
          isRecord(arrayChild) &&
          isInRange(cursorPosition, arrayChild)
        ) {
          return {
            key: [name, String(index)],
            value: arrayChild,
          };
        }
      }
    }
  }
  return null;
}
```
</details>

- **Parameters**:
  - `iter: object`
  - `cursorPosition: number`
  - `visited: Set<unknown>`
- **Return Type**: `{
  key: string[];
  value: unknown;
} | null`
- **Calls**:
  - `Object.entries`
  - `visited.has`
  - `isIterable`
  - `visited.add`
  - `isRecord (from ./utils)`
  - `isInRange`
  - `Array.isArray`
  - `String`
- **Internal Comments**:
```
// we do not want to select parents in case if we do filter with esquery
// typescript array like elements have other iterable items
```

### `findSelectionPath(node: object, cursorPosition: number): { node: object | null; path: string[] }`

<details><summary>Code</summary>

```ts
export function findSelectionPath(
  node: object,
  cursorPosition: number,
): { node: object | null; path: string[] } {
  const nodePath = ['ast'];
  const visited = new Set<unknown>();
  let currentNode: unknown = node;
  while (currentNode) {
    // infinite loop guard
    if (visited.has(currentNode)) {
      break;
    }
    visited.add(currentNode);

    const result = findInObject(currentNode, cursorPosition, visited);
    if (result) {
      currentNode = result.value;
      nodePath.push(...result.key);
    } else {
      return { node: currentNode, path: nodePath };
    }
  }
  return { node: null, path: nodePath };
}
```
</details>

- **Parameters**:
  - `node: object`
  - `cursorPosition: number`
- **Return Type**: `{ node: object | null; path: string[] }`
- **Calls**:
  - `visited.has`
  - `visited.add`
  - `findInObject`
  - `nodePath.push`
- **Internal Comments**:
```
// infinite loop guard
```


---