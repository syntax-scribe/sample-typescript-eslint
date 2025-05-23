[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `init-declarations.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 8
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/init-declarations.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `InferMessageIdsTypeFromRule` | `../util` |
| `InferOptionsTypeFromRule` | `../util` |
| `createRule` | `../util` |
| `getESLintCoreRule` | `../util/getESLintCoreRule` |


---

## Functions

### `getBaseContextOverride(): typeof context`

<details><summary>Code</summary>

```ts
function getBaseContextOverride(): typeof context {
      const reportOverride: typeof context.report = descriptor => {
        if ('node' in descriptor && descriptor.loc == null) {
          const { node, ...rest } = descriptor;
          // We only want to special case the report loc when reporting on
          // variables declarations that are not initialized. Declarations that
          // _are_ initialized get reported by the base rule due to a setting to
          // prohibit initializing variables entirely, in which case underlining
          // the whole node including the type annotation and initializer is
          // appropriate.
          if (
            node.type === AST_NODE_TYPES.VariableDeclarator &&
            node.init == null
          ) {
            context.report({
              ...rest,
              loc: getReportLoc(node),
            });
            return;
          }
        }

        context.report(descriptor);
      };

      // `return { ...context, report: reportOverride }` isn't safe because the
      // `context` object has some getters that need to be preserved.
      //
      // `return new Proxy(context, ...)` doesn't work because `context` has
      // non-configurable properties that throw when constructing a Proxy.
      //
      // So, we'll just use Proxy on a dummy object and use the `get` trap to
      // proxy `context`'s properties.
      return new Proxy({} as typeof context, {
        get: (target, prop, receiver): unknown =>
          prop === 'report'
            ? reportOverride
            : Reflect.get(context, prop, receiver),
      });
    }
```
</details>

- **Return Type**: `typeof context`
- **Calls**:
  - `context.report`
  - `getReportLoc`
  - `Reflect.get`
- **Internal Comments**:
```
// We only want to special case the report loc when reporting on
// variables declarations that are not initialized. Declarations that
// _are_ initialized get reported by the base rule due to a setting to
// prohibit initializing variables entirely, in which case underlining
// the whole node including the type annotation and initializer is
// appropriate.
// `return { ...context, report: reportOverride }` isn't safe because the
// `context` object has some getters that need to be preserved.
// (x2)
// `return new Proxy(context, ...)` doesn't work because `context` has
// non-configurable properties that throw when constructing a Proxy.
// So, we'll just use Proxy on a dummy object and use the `get` trap to
// proxy `context`'s properties.
```

### `reportOverride(descriptor: any): void`

<details><summary>Code</summary>

```ts
descriptor => {
        if ('node' in descriptor && descriptor.loc == null) {
          const { node, ...rest } = descriptor;
          // We only want to special case the report loc when reporting on
          // variables declarations that are not initialized. Declarations that
          // _are_ initialized get reported by the base rule due to a setting to
          // prohibit initializing variables entirely, in which case underlining
          // the whole node including the type annotation and initializer is
          // appropriate.
          if (
            node.type === AST_NODE_TYPES.VariableDeclarator &&
            node.init == null
          ) {
            context.report({
              ...rest,
              loc: getReportLoc(node),
            });
            return;
          }
        }

        context.report(descriptor);
      }
```
</details>

- **Parameters**:
  - `descriptor: any`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getReportLoc`
- **Internal Comments**:
```
// We only want to special case the report loc when reporting on
// variables declarations that are not initialized. Declarations that
// _are_ initialized get reported by the base rule due to a setting to
// prohibit initializing variables entirely, in which case underlining
// the whole node including the type annotation and initializer is
// appropriate.
```

### `get(target: any, prop: string | symbol, receiver: any): unknown`

<details><summary>Code</summary>

```ts
(target, prop, receiver): unknown =>
          prop === 'report'
            ? reportOverride
            : Reflect.get(context, prop, receiver)
```
</details>

- **Parameters**:
  - `target: any`
  - `prop: string | symbol`
  - `receiver: any`
- **Return Type**: `unknown`
### `get(target: any, prop: string | symbol, receiver: any): unknown`

<details><summary>Code</summary>

```ts
(target, prop, receiver): unknown =>
          prop === 'report'
            ? reportOverride
            : Reflect.get(context, prop, receiver)
```
</details>

- **Parameters**:
  - `target: any`
  - `prop: string | symbol`
  - `receiver: any`
- **Return Type**: `unknown`
### `isAncestorNamespaceDeclared(node: TSESTree.VariableDeclaration): boolean`

<details><summary>Code</summary>

```ts
function isAncestorNamespaceDeclared(
      node: TSESTree.VariableDeclaration,
    ): boolean {
      let ancestor: TSESTree.Node | undefined = node.parent;

      while (ancestor) {
        if (
          ancestor.type === AST_NODE_TYPES.TSModuleDeclaration &&
          ancestor.declare
        ) {
          return true;
        }

        ancestor = ancestor.parent;
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.VariableDeclaration`
- **Return Type**: `boolean`
### `get(target: any, prop: string | symbol, receiver: any): unknown`

<details><summary>Code</summary>

```ts
(target, prop, receiver): unknown =>
          prop === 'report'
            ? reportOverride
            : Reflect.get(context, prop, receiver)
```
</details>

- **Parameters**:
  - `target: any`
  - `prop: string | symbol`
  - `receiver: any`
- **Return Type**: `unknown`
### `get(target: any, prop: string | symbol, receiver: any): unknown`

<details><summary>Code</summary>

```ts
(target, prop, receiver): unknown =>
          prop === 'report'
            ? reportOverride
            : Reflect.get(context, prop, receiver)
```
</details>

- **Parameters**:
  - `target: any`
  - `prop: string | symbol`
  - `receiver: any`
- **Return Type**: `unknown`
### `getReportLoc(node: TSESTree.VariableDeclarator): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
function getReportLoc(
  node: TSESTree.VariableDeclarator,
): TSESTree.SourceLocation {
  const start: TSESTree.Position = structuredClone(node.loc.start);
  const end: TSESTree.Position = {
    line: node.loc.start.line,
    // `if (id.type === AST_NODE_TYPES.Identifier)` is a condition for
    // reporting in the base rule (as opposed to things like destructuring
    // assignment), so the type assertion should always be valid.
    column:
      node.loc.start.column + (node.id as TSESTree.Identifier).name.length,
  };

  return {
    start,
    end,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * When reporting an uninitialized variable declarator, get the loc excluding
 * the type annotation.
 */
```

- **Parameters**:
  - `node: TSESTree.VariableDeclarator`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `structuredClone`
- **Internal Comments**:
```
// `if (id.type === AST_NODE_TYPES.Identifier)` is a condition for (x2)
// reporting in the base rule (as opposed to things like destructuring (x2)
// assignment), so the type assertion should always be valid. (x2)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `Options`

```ts
type Options = InferOptionsTypeFromRule<typeof baseRule>;
```

### `MessageIds`

```ts
type MessageIds = InferMessageIdsTypeFromRule<typeof baseRule>;
```


---