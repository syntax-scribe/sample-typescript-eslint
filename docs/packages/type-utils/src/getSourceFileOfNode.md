[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getSourceFileOfNode.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/getSourceFileOfNode.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `getSourceFileOfNode(node: ts.Node): ts.SourceFile`

<details><summary>Code</summary>

```ts
export function getSourceFileOfNode(node: ts.Node): ts.SourceFile {
  while (node.kind !== ts.SyntaxKind.SourceFile) {
    node = node.parent;
  }
  return node as ts.SourceFile;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the source file for a given node
 */
```

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `ts.SourceFile`

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