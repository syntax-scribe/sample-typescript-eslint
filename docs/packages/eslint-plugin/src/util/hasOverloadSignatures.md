[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `hasOverloadSignatures.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/hasOverloadSignatures.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `getStaticMemberAccessValue` | `./misc` |


---

## Functions

### `hasOverloadSignatures(node: TSESTree.FunctionDeclaration | TSESTree.MethodDefinition, context: RuleContext<string, unknown[]>): boolean`

<details><summary>Code</summary>

```ts
export function hasOverloadSignatures(
  node: TSESTree.FunctionDeclaration | TSESTree.MethodDefinition,
  context: RuleContext<string, unknown[]>,
): boolean {
  // `export default function () {}`
  if (node.parent.type === AST_NODE_TYPES.ExportDefaultDeclaration) {
    return node.parent.parent.body.some(member => {
      return (
        member.type === AST_NODE_TYPES.ExportDefaultDeclaration &&
        member.declaration.type === AST_NODE_TYPES.TSDeclareFunction
      );
    });
  }

  // `export function f() {}`
  if (node.parent.type === AST_NODE_TYPES.ExportNamedDeclaration) {
    return node.parent.parent.body.some(member => {
      return (
        member.type === AST_NODE_TYPES.ExportNamedDeclaration &&
        member.declaration?.type === AST_NODE_TYPES.TSDeclareFunction &&
        getFunctionDeclarationName(member.declaration, context) ===
          getFunctionDeclarationName(node, context)
      );
    });
  }

  // either:
  // - `function f() {}`
  // - `class T { foo() {} }`

  const nodeKey = getFunctionDeclarationName(node, context);

  return node.parent.body.some(member => {
    return (
      (member.type === AST_NODE_TYPES.TSDeclareFunction ||
        (member.type === AST_NODE_TYPES.MethodDefinition &&
          member.value.body == null)) &&
      nodeKey === getFunctionDeclarationName(member, context)
    );
  });
}
```
</details>

- **JSDoc**:
```ts
/**
 * @return `true` if the function or method node has overload signatures.
 */
```

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration | TSESTree.MethodDefinition`
  - `context: RuleContext<string, unknown[]>`
- **Return Type**: `boolean`
- **Calls**:
  - `node.parent.parent.body.some`
  - `getFunctionDeclarationName`
  - `node.parent.body.some`
- **Internal Comments**:
```
// `export default function () {}`
// `export function f() {}`
// either: (x2)
// - `function f() {}` (x2)
// - `class T { foo() {} }` (x2)
```

### `getFunctionDeclarationName(node: | TSESTree.FunctionDeclaration
    | TSESTree.MethodDefinition
    | TSESTree.TSDeclareFunction, context: RuleContext<string, unknown[]>): string | symbol | undefined`

<details><summary>Code</summary>

```ts
function getFunctionDeclarationName(
  node:
    | TSESTree.FunctionDeclaration
    | TSESTree.MethodDefinition
    | TSESTree.TSDeclareFunction,
  context: RuleContext<string, unknown[]>,
): string | symbol | undefined {
  if (
    node.type === AST_NODE_TYPES.FunctionDeclaration ||
    node.type === AST_NODE_TYPES.TSDeclareFunction
  ) {
    // For a `FunctionDeclaration` or `TSDeclareFunction` this may be `null` if
    // and only if the parent is an `ExportDefaultDeclaration`.
    //
    // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
    return node.id!.name;
  }

  return getStaticMemberAccessValue(node, context);
}
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
    | TSESTree.MethodDefinition
    | TSESTree.TSDeclareFunction`
  - `context: RuleContext<string, unknown[]>`
- **Return Type**: `string | symbol | undefined`
- **Calls**:
  - `getStaticMemberAccessValue (from ./misc)`
- **Internal Comments**:
```
// For a `FunctionDeclaration` or `TSDeclareFunction` this may be `null` if
// and only if the parent is an `ExportDefaultDeclaration`.
//
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion
```


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