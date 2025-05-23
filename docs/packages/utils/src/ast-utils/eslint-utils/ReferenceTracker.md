[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ReferenceTracker.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 4
- **Type Aliases**: 6

## 🛠️ File Location:
📂 **`packages/utils/src/ast-utils/eslint-utils/ReferenceTracker.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `../../ts-estree` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ReferenceTracker`

<details><summary>Interface Code</summary>

```ts
interface ReferenceTracker {
  /**
   * Iterate the references that the given `traceMap` determined.
   * This method starts to search from `require()` expression.
   *
   * @see {@link https://eslint-community.github.io/eslint-utils/api/scope-utils.html#tracker-iteratecjsreferences}
   */
  iterateCjsReferences<T>(
    traceMap: ReferenceTracker.TraceMap<T>,
  ): IterableIterator<ReferenceTracker.FoundReference<T>>;

  /**
   * Iterate the references that the given `traceMap` determined.
   * This method starts to search from `import`/`export` declarations.
   *
   * @see {@link https://eslint-community.github.io/eslint-utils/api/scope-utils.html#tracker-iterateesmreferences}
   */
  iterateEsmReferences<T>(
    traceMap: ReferenceTracker.TraceMap<T>,
  ): IterableIterator<ReferenceTracker.FoundReference<T>>;

  /**
   * Iterate the references that the given `traceMap` determined.
   * This method starts to search from global variables.
   *
   * @see {@link https://eslint-community.github.io/eslint-utils/api/scope-utils.html#tracker-iterateglobalreferences}
   */
  iterateGlobalReferences<T>(
    traceMap: ReferenceTracker.TraceMap<T>,
  ): IterableIterator<ReferenceTracker.FoundReference<T>>;
}
```
</details>

### `ReferenceTrackerStatic`

<details><summary>Interface Code</summary>

```ts
interface ReferenceTrackerStatic {
  readonly CALL: typeof ReferenceTrackerCALL;
  readonly CONSTRUCT: typeof ReferenceTrackerCONSTRUCT;
  readonly ESM: typeof ReferenceTrackerESM;

  new (
    globalScope: TSESLint.Scope.Scope,
    options?: {
      /**
       * The name list of Global Object. Optional. Default is `["global", "globalThis", "self", "window"]`.
       */
      globalObjectNames?: readonly string[];
      /**
       * The mode which determines how the `tracker.iterateEsmReferences()` method scans CommonJS modules.
       * If this is `"strict"`, the method binds CommonJS modules to the default export. Otherwise, the method binds
       * CommonJS modules to both the default export and named exports. Optional. Default is `"strict"`.
       */
      mode?: 'legacy' | 'strict';
    },
  ): ReferenceTracker;

  readonly READ: typeof ReferenceTrackerREAD;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `CALL` | `typeof ReferenceTrackerCALL` | ✗ |  |
| `CONSTRUCT` | `typeof ReferenceTrackerCONSTRUCT` | ✗ |  |
| `ESM` | `typeof ReferenceTrackerESM` | ✗ |  |
| `READ` | `typeof ReferenceTrackerREAD` | ✗ |  |

### `TraceMapElement<T>`

<details><summary>Interface Code</summary>

```ts
export interface TraceMapElement<T> {
    [key: string]: TraceMapElement<T>;
    [ReferenceTrackerCALL]?: T;
    [ReferenceTrackerCONSTRUCT]?: T;
    [ReferenceTrackerESM]?: true;
    [ReferenceTrackerREAD]?: T;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[ReferenceTrackerCALL]` | `T` | ✓ |  |
| `[ReferenceTrackerCONSTRUCT]` | `T` | ✓ |  |
| `[ReferenceTrackerESM]` | `true` | ✓ |  |
| `[ReferenceTrackerREAD]` | `T` | ✓ |  |

### `FoundReference<T = any>`

<details><summary>Interface Code</summary>

```ts
export interface FoundReference<T = any> {
    info: T;
    node: TSESTree.Node;
    path: readonly string[];
    type: ReferenceType;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `info` | `T` | ✗ |  |
| `node` | `TSESTree.Node` | ✗ |  |
| `path` | `readonly string[]` | ✗ |  |
| `type` | `ReferenceType` | ✗ |  |


---

## Type Aliases

### `READ`

```ts
type READ = ReferenceTrackerStatic['READ'];
```

### `CALL`

```ts
type CALL = ReferenceTrackerStatic['CALL'];
```

### `CONSTRUCT`

```ts
type CONSTRUCT = ReferenceTrackerStatic['CONSTRUCT'];
```

### `ESM`

```ts
type ESM = ReferenceTrackerStatic['ESM'];
```

### `ReferenceType`

```ts
type ReferenceType = CALL | CONSTRUCT | READ;
```

### `TraceMap<T = any = any>`

```ts
type TraceMap<T = any = any> = Record<string, TraceMapElement<T>>;
```


---