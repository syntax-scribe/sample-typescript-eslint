[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

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