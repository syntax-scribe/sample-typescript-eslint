[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `LeftHandSideExpression.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 21
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/LeftHandSideExpression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ArrayExpression` | `../expression/ArrayExpression/spec` |
| `ArrowFunctionExpression` | `../expression/ArrowFunctionExpression/spec` |
| `CallExpression` | `../expression/CallExpression/spec` |
| `ClassExpression` | `../expression/ClassExpression/spec` |
| `FunctionExpression` | `../expression/FunctionExpression/spec` |
| `Identifier` | `../expression/Identifier/spec` |
| `JSXElement` | `../expression/JSXElement/spec` |
| `JSXFragment` | `../expression/JSXFragment/spec` |
| `MemberExpression` | `../expression/MemberExpression/spec` |
| `MetaProperty` | `../expression/MetaProperty/spec` |
| `ObjectExpression` | `../expression/ObjectExpression/spec` |
| `SequenceExpression` | `../expression/spec` |
| `Super` | `../expression/Super/spec` |
| `TaggedTemplateExpression` | `../expression/TaggedTemplateExpression/spec` |
| `ThisExpression` | `../expression/ThisExpression/spec` |
| `TSAsExpression` | `../expression/TSAsExpression/spec` |
| `TSNonNullExpression` | `../expression/TSNonNullExpression/spec` |
| `TSTypeAssertion` | `../expression/TSTypeAssertion/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
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

### `LeftHandSideExpression`

```ts
type LeftHandSideExpression = | ArrayExpression
  | ArrayPattern
  | ArrowFunctionExpression
  | CallExpression
  | ClassExpression
  | FunctionExpression
  | Identifier
  | JSXElement
  | JSXFragment
  | LiteralExpression
  | MemberExpression
  | MetaProperty
  | ObjectExpression
  | ObjectPattern
  | SequenceExpression
  | Super
  | TaggedTemplateExpression
  | ThisExpression
  | TSAsExpression
  | TSNonNullExpression
  | TSTypeAssertion;
```


---