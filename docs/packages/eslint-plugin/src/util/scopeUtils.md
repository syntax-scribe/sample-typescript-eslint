[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `scopeUtils.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/scopeUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |


---

## Functions

### `isReferenceToGlobalFunction(calleeName: string, node: TSESTree.Node, sourceCode: SourceCode): boolean`

<details><summary>Code</summary>

```ts
export function isReferenceToGlobalFunction(
  calleeName: string,
  node: TSESTree.Node,
  sourceCode: SourceCode,
): boolean {
  const ref = sourceCode
    .getScope(node)
    .references.find(ref => ref.identifier.name === calleeName);

  // ensure it's the "global" version
  return !ref?.resolved?.defs.length;
}
```
</details>

- **Parameters**:
  - `calleeName: string`
  - `node: TSESTree.Node`
  - `sourceCode: SourceCode`
- **Return Type**: `boolean`
- **Calls**:
  - `sourceCode
    .getScope(node)
    .references.find`
- **Internal Comments**:
```
// ensure it's the "global" version
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