[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `LeftHandSideExpression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 21 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

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