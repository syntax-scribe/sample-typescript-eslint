[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getSourceFileOfNode.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/getSourceFileOfNode.ts`**

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