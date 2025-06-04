[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/Program/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `NodeOrTokenData` | `../../base/NodeOrTokenData` |
| `Comment` | `../../unions/Comment` |
| `ProgramStatement` | `../../unions/Statement` |
| `Token` | `../../unions/Token` |


---


---

## Interfaces

### `Program`

<details><summary>Interface Code</summary>

```ts
export interface Program extends NodeOrTokenData {
  type: AST_NODE_TYPES.Program;
  body: ProgramStatement[];
  comments: Comment[] | undefined;
  sourceType: 'module' | 'script';
  tokens: Token[] | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Program` | ✗ |  |
| `body` | `ProgramStatement[]` | ✗ |  |
| `comments` | `Comment[] | undefined` | ✗ |  |
| `sourceType` | `'module' | 'script'` | ✗ |  |
| `tokens` | `Token[] | undefined` | ✗ |  |


---