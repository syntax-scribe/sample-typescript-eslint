[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ts-nodes.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 6 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/ts-estree/ts-nodes.ts`**


---

## Interfaces

### `AssertClause`

<details><summary>Interface Code</summary>

```ts
export interface AssertClause extends ts.ImportAttributes {}
```
</details>

### `AssertEntry`

<details><summary>Interface Code</summary>

```ts
export interface AssertEntry extends ts.ImportAttribute {}
```
</details>

### `SatisfiesExpression`

<details><summary>Interface Code</summary>

```ts
export interface SatisfiesExpression extends ts.Node {}
```
</details>

### `JsxNamespacedName`

<details><summary>Interface Code</summary>

```ts
export interface JsxNamespacedName extends ts.Node {}
```
</details>

### `ImportAttribute`

<details><summary>Interface Code</summary>

```ts
export interface ImportAttribute extends ts.Node {}
```
</details>

### `ImportAttributes`

<details><summary>Interface Code</summary>

```ts
export interface ImportAttributes extends ts.Node {}
```
</details>


---

## Type Aliases

### `TSToken`

```ts
type TSToken = ts.Token<ts.SyntaxKind>;
```

### `TSNode`

```ts
type TSNode = | ts.ArrayBindingPattern
  | ts.ArrayLiteralExpression
  | ts.ArrayTypeNode
  | ts.ArrowFunction
  | ts.AsExpression
  /* eslint-disable-next-line @typescript-eslint/no-deprecated -- intentional for old TS versions */
  | ts.AssertClause
  /* eslint-disable-next-line @typescript-eslint/no-deprecated -- intentional for old TS versions */
  | ts.AssertEntry
  | ts.AwaitExpression
  | ts.BigIntLiteral
  | ts.BinaryExpression
  | ts.BindingElement
  | ts.Block
  | ts.BooleanLiteral
  | ts.BreakStatement
  | ts.Bundle
  | ts.CallExpression
  | ts.CallSignatureDeclaration
  | ts.CaseBlock
  | ts.CaseClause
  | ts.CatchClause
  | ts.ClassDeclaration
  | ts.ClassExpression
  // | ts.ClassLikeDeclarationBase -> ClassDeclaration | ClassExpression
  | ts.ClassStaticBlockDeclaration
  | ts.CommaListExpression
  | ts.ComputedPropertyName
  | ts.ConditionalExpression
  | ts.ConditionalTypeNode
  | ts.ConstructorDeclaration
  | ts.ConstructorTypeNode
  | ts.ConstructSignatureDeclaration
  | ts.ContinueStatement
  | ts.DebuggerStatement
  | ts.Decorator
  | ts.DefaultClause
  | ts.DeleteExpression
  | ts.DoStatement
  | ts.ElementAccessExpression
  | ts.EmptyStatement
  | ts.EnumDeclaration
  | ts.EnumMember
  | ts.ExportAssignment
  | ts.ExportDeclaration
  | ts.ExportSpecifier
  | ts.ExpressionStatement
  | ts.ExpressionWithTypeArguments
  | ts.ExternalModuleReference
  | ts.ForInStatement
  | ts.ForOfStatement
  | ts.ForStatement
  | ts.FunctionDeclaration
  | ts.FunctionExpression
  // | ts.FunctionOrConstructorTypeNodeBase -> FunctionTypeNode, ConstructorTypeNode
  | ts.FunctionTypeNode
  | ts.GetAccessorDeclaration
  | ts.HeritageClause
  | ts.Identifier
  | ts.IfStatement
  | ts.ImportAttribute
  | ts.ImportAttributes
  | ts.ImportClause
  | ts.ImportDeclaration
  | ts.ImportEqualsDeclaration
  | ts.ImportExpression
  | ts.ImportSpecifier
  | ts.ImportTypeNode
  | ts.IndexedAccessTypeNode
  | ts.IndexSignatureDeclaration
  | ts.InferTypeNode
  | ts.InterfaceDeclaration
  | ts.IntersectionTypeNode
  | ts.JSDoc
  | ts.JSDocAllType
  | ts.JSDocAugmentsTag
  | ts.JSDocAuthorTag
  | ts.JSDocCallbackTag
  | ts.JSDocClassTag
  | ts.JSDocEnumTag
  | ts.JSDocFunctionType
  | ts.JSDocNonNullableType
  | ts.JSDocNullableType
  | ts.JSDocOptionalType
  | ts.JSDocParameterTag
  | ts.JSDocPropertyTag
  | ts.JSDocReturnTag
  | ts.JSDocSignature
  | ts.JSDocTemplateTag
  | ts.JSDocThisTag
  | ts.JSDocTypedefTag
  | ts.JSDocTypeExpression
  | ts.JSDocTypeLiteral
  | ts.JSDocTypeTag
  | ts.JSDocUnknownTag
  | ts.JSDocUnknownType
  | ts.JSDocVariadicType
  | ts.JsonMinusNumericLiteral
  | ts.JsxAttribute
  | ts.JsxClosingElement
  | ts.JsxClosingFragment
  | ts.JsxElement
  | ts.JsxExpression
  | ts.JsxFragment
  | ts.JsxNamespacedName
  | ts.JsxOpeningElement
  | ts.JsxOpeningFragment
  | ts.JsxSelfClosingElement
  | ts.JsxSpreadAttribute
  | ts.JsxText
  | ts.KeywordTypeNode // TODO: This node is bad, maybe we should report this
  | ts.LabeledStatement
  | ts.LiteralTypeNode
  | ts.MappedTypeNode
  | ts.MetaProperty
  | ts.MethodDeclaration
  | ts.MethodSignature
  | ts.MissingDeclaration
  | ts.Modifier
  | ts.ModuleBlock
  | ts.ModuleDeclaration
  | ts.NamedExports
  | ts.NamedImports
  | ts.NamedTupleMember
  | ts.NamespaceExportDeclaration
  | ts.NamespaceImport
  | ts.NewExpression
  | ts.NonNullExpression
  | ts.NoSubstitutionTemplateLiteral
  | ts.NotEmittedStatement
  | ts.NullLiteral
  | ts.NumericLiteral
  | ts.ObjectBindingPattern
  | ts.ObjectLiteralExpression
  | ts.OmittedExpression
  | ts.OptionalTypeNode
  | ts.ParameterDeclaration
  | ts.ParenthesizedExpression
  | ts.ParenthesizedTypeNode
  | ts.PartiallyEmittedExpression
  | ts.PostfixUnaryExpression
  | ts.PrefixUnaryExpression
  | ts.PrivateIdentifier
  | ts.PropertyAccessExpression
  | ts.PropertyAssignment
  | ts.PropertyDeclaration
  | ts.PropertySignature
  | ts.QualifiedName
  | ts.RegularExpressionLiteral
  | ts.RestTypeNode
  | ts.ReturnStatement
  | ts.SatisfiesExpression
  | ts.SemicolonClassElement
  | ts.SetAccessorDeclaration
  // | ts.SignatureDeclarationBase -> CallSignatureDeclaration, ConstructSignatureDeclaration
  | ts.ShorthandPropertyAssignment
  | ts.SourceFile
  | ts.SpreadAssignment
  | ts.SpreadElement
  | ts.StringLiteral
  | ts.SuperExpression
  | ts.SwitchStatement
  | ts.SyntheticExpression
  | ts.TaggedTemplateExpression
  | ts.TemplateExpression
  | ts.TemplateHead
  | ts.TemplateLiteralTypeNode
  | ts.TemplateMiddle

  // JSDoc: Unsupported
  | ts.TemplateSpan
  | ts.TemplateTail
  | ts.ThisExpression
  | ts.ThisTypeNode
  | ts.ThrowStatement
  | ts.TryStatement
  | ts.TupleTypeNode
  | ts.TypeAliasDeclaration
  | ts.TypeAssertion
  | ts.TypeLiteralNode
  | ts.TypeOfExpression
  | ts.TypeOperatorNode
  | ts.TypeParameterDeclaration
  | ts.TypePredicateNode
  | ts.TypeQueryNode
  | ts.TypeReferenceNode
  | ts.UnionTypeNode
  | ts.VariableDeclaration
  | ts.VariableDeclarationList
  | ts.VariableStatement
  | ts.VoidExpression
  | ts.WhileStatement
  | ts.WithStatement
  | ts.YieldExpression;
```


---