[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `scopeUtils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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

- [Imports](#imports)
- [Functions](#functions)

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