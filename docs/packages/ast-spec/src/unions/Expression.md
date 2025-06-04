[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Expression.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 35 |
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
📂 **`packages/ast-spec/src/unions/Expression.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ArrayExpression` | `../expression/ArrayExpression/spec` |
| `ArrowFunctionExpression` | `../expression/ArrowFunctionExpression/spec` |
| `AssignmentExpression` | `../expression/AssignmentExpression/spec` |
| `AwaitExpression` | `../expression/AwaitExpression/spec` |
| `BinaryExpression` | `../expression/BinaryExpression/spec` |
| `CallExpression` | `../expression/CallExpression/spec` |
| `ChainExpression` | `../expression/ChainExpression/spec` |
| `ClassExpression` | `../expression/ClassExpression/spec` |
| `ConditionalExpression` | `../expression/ConditionalExpression/spec` |
| `FunctionExpression` | `../expression/FunctionExpression/spec` |
| `Identifier` | `../expression/Identifier/spec` |
| `ImportExpression` | `../expression/ImportExpression/spec` |
| `JSXElement` | `../expression/JSXElement/spec` |
| `JSXFragment` | `../expression/JSXFragment/spec` |
| `LogicalExpression` | `../expression/LogicalExpression/spec` |
| `MemberExpression` | `../expression/MemberExpression/spec` |
| `MetaProperty` | `../expression/MetaProperty/spec` |
| `NewExpression` | `../expression/NewExpression/spec` |
| `ObjectExpression` | `../expression/ObjectExpression/spec` |
| `SequenceExpression` | `../expression/SequenceExpression/spec` |
| `Super` | `../expression/Super/spec` |
| `TaggedTemplateExpression` | `../expression/TaggedTemplateExpression/spec` |
| `TemplateLiteral` | `../expression/TemplateLiteral/spec` |
| `ThisExpression` | `../expression/ThisExpression/spec` |
| `TSAsExpression` | `../expression/TSAsExpression/spec` |
| `TSInstantiationExpression` | `../expression/TSInstantiationExpression/spec` |
| `TSNonNullExpression` | `../expression/TSNonNullExpression/spec` |
| `TSSatisfiesExpression` | `../expression/TSSatisfiesExpression/spec` |
| `TSTypeAssertion` | `../expression/TSTypeAssertion/spec` |
| `UnaryExpression` | `../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../expression/UpdateExpression/spec` |
| `YieldExpression` | `../expression/YieldExpression/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
| `LiteralExpression` | `./LiteralExpression` |


---


---

## Type Aliases

### `Expression`

```ts
type Expression = | ArrayExpression
  | ArrayPattern
  | ArrowFunctionExpression
  | AssignmentExpression
  | AwaitExpression
  | BinaryExpression
  | CallExpression
  | ChainExpression
  | ClassExpression
  | ConditionalExpression
  | FunctionExpression
  | Identifier
  | ImportExpression
  | JSXElement
  | JSXFragment
  | LiteralExpression
  | LogicalExpression
  | MemberExpression
  | MetaProperty
  | NewExpression
  | ObjectExpression
  | ObjectPattern
  | SequenceExpression
  | Super
  | TaggedTemplateExpression
  | TemplateLiteral
  | ThisExpression
  | TSAsExpression
  | TSInstantiationExpression
  | TSNonNullExpression
  | TSSatisfiesExpression
  | TSTypeAssertion
  | UnaryExpression
  | UpdateExpression
  | YieldExpression;
```


---