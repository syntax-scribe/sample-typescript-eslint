[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `visitor-keys.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/visitor-keys/src/visitor-keys.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |


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

### `VisitorKeys`

```ts
type VisitorKeys = Record<string, readonly string[] | undefined>;
```

### `GetNodeTypeKeys<T extends AST_NODE_TYPES extends AST_NODE_TYPES>`

```ts
type GetNodeTypeKeys<T extends AST_NODE_TYPES extends AST_NODE_TYPES> = Exclude<
  keyof Extract<TSESTree.Node, { type: T }>,
  'loc' | 'parent' | 'range' | 'type'
>;
```

### `KeysDefinedInESLintVisitorKeysCore`

```ts
type KeysDefinedInESLintVisitorKeysCore = | AST_NODE_TYPES.ArrayExpression
  | AST_NODE_TYPES.ArrayPattern
  | AST_NODE_TYPES.ArrowFunctionExpression
  | AST_NODE_TYPES.AssignmentExpression
  | AST_NODE_TYPES.AssignmentPattern
  | AST_NODE_TYPES.AwaitExpression
  | AST_NODE_TYPES.BinaryExpression
  | AST_NODE_TYPES.BlockStatement
  | AST_NODE_TYPES.BreakStatement
  | AST_NODE_TYPES.CallExpression
  | AST_NODE_TYPES.CatchClause
  | AST_NODE_TYPES.ChainExpression
  | AST_NODE_TYPES.ClassBody
  | AST_NODE_TYPES.ClassDeclaration
  | AST_NODE_TYPES.ClassExpression
  | AST_NODE_TYPES.ConditionalExpression
  | AST_NODE_TYPES.ContinueStatement
  | AST_NODE_TYPES.DebuggerStatement
  | AST_NODE_TYPES.DoWhileStatement
  | AST_NODE_TYPES.EmptyStatement
  | AST_NODE_TYPES.ExportAllDeclaration
  | AST_NODE_TYPES.ExportDefaultDeclaration
  | AST_NODE_TYPES.ExportNamedDeclaration
  | AST_NODE_TYPES.ExportSpecifier
  | AST_NODE_TYPES.ExpressionStatement
  | AST_NODE_TYPES.ForInStatement
  | AST_NODE_TYPES.ForOfStatement
  | AST_NODE_TYPES.ForStatement
  | AST_NODE_TYPES.FunctionDeclaration
  | AST_NODE_TYPES.FunctionExpression
  | AST_NODE_TYPES.Identifier
  | AST_NODE_TYPES.IfStatement
  | AST_NODE_TYPES.ImportDeclaration
  | AST_NODE_TYPES.ImportDefaultSpecifier
  | AST_NODE_TYPES.ImportExpression
  | AST_NODE_TYPES.ImportNamespaceSpecifier
  | AST_NODE_TYPES.ImportSpecifier
  | AST_NODE_TYPES.JSXAttribute
  | AST_NODE_TYPES.JSXClosingElement
  | AST_NODE_TYPES.JSXClosingFragment
  | AST_NODE_TYPES.JSXElement
  | AST_NODE_TYPES.JSXEmptyExpression
  | AST_NODE_TYPES.JSXExpressionContainer
  | AST_NODE_TYPES.JSXFragment
  | AST_NODE_TYPES.JSXIdentifier
  | AST_NODE_TYPES.JSXMemberExpression
  | AST_NODE_TYPES.JSXNamespacedName
  | AST_NODE_TYPES.JSXOpeningElement
  | AST_NODE_TYPES.JSXOpeningFragment
  | AST_NODE_TYPES.JSXSpreadAttribute
  | AST_NODE_TYPES.JSXText
  | AST_NODE_TYPES.LabeledStatement
  | AST_NODE_TYPES.Literal
  | AST_NODE_TYPES.LogicalExpression
  | AST_NODE_TYPES.MemberExpression
  | AST_NODE_TYPES.MetaProperty
  | AST_NODE_TYPES.MethodDefinition
  | AST_NODE_TYPES.NewExpression
  | AST_NODE_TYPES.ObjectExpression
  | AST_NODE_TYPES.ObjectPattern
  | AST_NODE_TYPES.PrivateIdentifier
  | AST_NODE_TYPES.Program
  | AST_NODE_TYPES.Property
  | AST_NODE_TYPES.PropertyDefinition
  | AST_NODE_TYPES.RestElement
  | AST_NODE_TYPES.ReturnStatement
  | AST_NODE_TYPES.SequenceExpression
  | AST_NODE_TYPES.SpreadElement
  | AST_NODE_TYPES.StaticBlock
  | AST_NODE_TYPES.Super
  | AST_NODE_TYPES.SwitchCase
  | AST_NODE_TYPES.SwitchStatement
  | AST_NODE_TYPES.TaggedTemplateExpression
  | AST_NODE_TYPES.TemplateElement
  | AST_NODE_TYPES.TemplateLiteral
  | AST_NODE_TYPES.ThisExpression
  | AST_NODE_TYPES.ThrowStatement
  | AST_NODE_TYPES.TryStatement
  | AST_NODE_TYPES.UnaryExpression
  | AST_NODE_TYPES.UpdateExpression
  | AST_NODE_TYPES.VariableDeclaration
  | AST_NODE_TYPES.VariableDeclarator
  | AST_NODE_TYPES.WhileStatement
  | AST_NODE_TYPES.WithStatement
  | AST_NODE_TYPES.YieldExpression;
```

### `AdditionalKeys`

```ts
type AdditionalKeys = {
  // optionally allow keys for all nodes defined in `eslint-visitor-keys`
  readonly [T in KeysDefinedInESLintVisitorKeysCore]?: readonly GetNodeTypeKeys<T>[];
} & {
  // require keys for all nodes NOT defined in `eslint-visitor-keys`
  readonly [T in Exclude<
    AST_NODE_TYPES,
    KeysDefinedInESLintVisitorKeysCore
  >]: readonly GetNodeTypeKeys<T>[];
};
```


---