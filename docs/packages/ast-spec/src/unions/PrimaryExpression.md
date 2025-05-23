[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `PrimaryExpression.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 16
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/PrimaryExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ArrayExpression` | `../expression/ArrayExpression/spec` |
| `ClassExpression` | `../expression/ClassExpression/spec` |
| `FunctionExpression` | `../expression/FunctionExpression/spec` |
| `Identifier` | `../expression/Identifier/spec` |
| `JSXElement` | `../expression/JSXElement/spec` |
| `JSXFragment` | `../expression/JSXFragment/spec` |
| `MetaProperty` | `../expression/MetaProperty/spec` |
| `ObjectExpression` | `../expression/ObjectExpression/spec` |
| `Super` | `../expression/Super/spec` |
| `TemplateLiteral` | `../expression/TemplateLiteral/spec` |
| `ThisExpression` | `../expression/ThisExpression/spec` |
| `JSXOpeningElement` | `../jsx/JSXOpeningElement/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
| `TSNullKeyword` | `../type/TSNullKeyword/spec` |
| `LiteralExpression` | `./LiteralExpression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `PrimaryExpression`

```ts
type PrimaryExpression = | ArrayExpression
  | ArrayPattern
  | ClassExpression
  | FunctionExpression
  | Identifier
  | JSXElement
  | JSXFragment
  | JSXOpeningElement
  | LiteralExpression
  | MetaProperty
  | ObjectExpression
  | ObjectPattern
  | Super
  | TemplateLiteral
  | ThisExpression
  | TSNullKeyword;
```


---