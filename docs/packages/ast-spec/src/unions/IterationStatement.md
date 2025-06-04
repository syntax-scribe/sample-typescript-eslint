[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `IterationStatement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/IterationStatement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `DoWhileStatement` | `../statement/DoWhileStatement/spec` |
| `ForInStatement` | `../statement/ForInStatement/spec` |
| `ForOfStatement` | `../statement/ForOfStatement/spec` |
| `ForStatement` | `../statement/ForStatement/spec` |
| `WhileStatement` | `../statement/WhileStatement/spec` |


---

## Type Aliases

### `IterationStatement`

```ts
type IterationStatement = | DoWhileStatement
  | ForInStatement
  | ForOfStatement
  | ForStatement
  | WhileStatement;
```


---