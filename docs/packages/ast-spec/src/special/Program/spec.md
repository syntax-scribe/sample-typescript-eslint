[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---