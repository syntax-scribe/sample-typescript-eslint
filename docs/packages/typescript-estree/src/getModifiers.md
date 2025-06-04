[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getModifiers.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/getModifiers.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `typescriptVersionIsAtLeast` | `./version-check` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `isAtLeast48` | `boolean` | const | `typescriptVersionIsAtLeast['4.8']` | ✗ |


---

## Functions

### `getModifiers(node: ts.Node | null | undefined, includeIllegalModifiers: boolean): ts.Modifier[] | undefined`

<details><summary>Code</summary>

```ts
export function getModifiers(
  node: ts.Node | null | undefined,
  includeIllegalModifiers = false,
): ts.Modifier[] | undefined {
  if (node == null) {
    return undefined;
  }

  if (isAtLeast48) {
    // eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded
    if (includeIllegalModifiers || ts.canHaveModifiers(node)) {
      // eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded
      const modifiers = ts.getModifiers(node as ts.HasModifiers);
      return modifiers ? [...modifiers] : undefined;
    }

    return undefined;
  }

  return (
    // @ts-expect-error intentional fallback for older TS versions
    (node.modifiers as ts.Modifier[] | undefined)?.filter(
      (m): m is ts.Modifier => !ts.isDecorator(m),
    )
  );
}
```
</details>

- **Parameters**:
  - `node: ts.Node | null | undefined`
  - `includeIllegalModifiers: boolean`
- **Return Type**: `ts.Modifier[] | undefined`
- **Calls**:
  - `ts.canHaveModifiers`
  - `ts.getModifiers`
  - `(node.modifiers as ts.Modifier[] | undefined)?.filter`
  - `ts.isDecorator`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded (x3)
// @ts-expect-error intentional fallback for older TS versions (x3)
```

### `getDecorators(node: ts.Node | null | undefined, includeIllegalDecorators: boolean): ts.Decorator[] | undefined`

<details><summary>Code</summary>

```ts
export function getDecorators(
  node: ts.Node | null | undefined,
  includeIllegalDecorators = false,
): ts.Decorator[] | undefined {
  if (node == null) {
    return undefined;
  }

  if (isAtLeast48) {
    // eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded
    if (includeIllegalDecorators || ts.canHaveDecorators(node)) {
      // eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded
      const decorators = ts.getDecorators(node as ts.HasDecorators);
      return decorators ? [...decorators] : undefined;
    }

    return undefined;
  }

  return (
    // @ts-expect-error intentional fallback for older TS versions
    (node.decorators as ts.Node[] | undefined)?.filter(ts.isDecorator)
  );
}
```
</details>

- **Parameters**:
  - `node: ts.Node | null | undefined`
  - `includeIllegalDecorators: boolean`
- **Return Type**: `ts.Decorator[] | undefined`
- **Calls**:
  - `ts.canHaveDecorators`
  - `ts.getDecorators`
  - `(node.decorators as ts.Node[] | undefined)?.filter`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-deprecated -- this is safe as it's guarded (x3)
// @ts-expect-error intentional fallback for older TS versions (x3)
```


---