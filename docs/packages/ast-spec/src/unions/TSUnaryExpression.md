[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSUnaryExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/TSUnaryExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AwaitExpression` | `../expression/AwaitExpression/spec` |
| `UnaryExpression` | `../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../expression/UpdateExpression/spec` |
| `LeftHandSideExpression` | `./LeftHandSideExpression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Type Aliases

### `TSUnaryExpression`

```ts
type TSUnaryExpression = | AwaitExpression
  | LeftHandSideExpression
  | UnaryExpression
  | UpdateExpression;
```


---