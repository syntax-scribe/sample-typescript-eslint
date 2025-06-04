[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `estree-to-ts-node-types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/ts-estree/estree-to-ts-node-types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `TSNode` | `./ts-nodes` |


---


---

## Interfaces

### `EstreeToTsNodeTypes`

<details><summary>Interface Code</summary>

```ts
export interface EstreeToTsNodeTypes {
  [AST_NODE_TYPES.AccessorProperty]: ts.PropertyDeclaration;
  [AST_NODE_TYPES.ArrayExpression]: ts.ArrayLiteralExpression;
  [AST_NODE_TYPES.ArrayPattern]:
    | ts.ArrayBindingPattern
    | ts.ArrayLiteralExpression;
  [AST_NODE_TYPES.ArrowFunctionExpression]: ts.ArrowFunction;
  [AST_NODE_TYPES.AssignmentExpression]: ts.BinaryExpression;
  [AST_NODE_TYPES.AssignmentPattern]:
    | ts.BinaryExpression
    | ts.BindingElement
    | ts.ParameterDeclaration
    | ts.ShorthandPropertyAssignment;
  [AST_NODE_TYPES.AwaitExpression]: ts.AwaitExpression;
  [AST_NODE_TYPES.BinaryExpression]: ts.BinaryExpression;
  [AST_NODE_TYPES.BlockStatement]: ts.Block;
  [AST_NODE_TYPES.BreakStatement]: ts.BreakStatement;
  [AST_NODE_TYPES.CallExpression]: ts.CallExpression;
  [AST_NODE_TYPES.CatchClause]: ts.CatchClause;
  [AST_NODE_TYPES.ChainExpression]:
    | ts.CallExpression
    | ts.ElementAccessExpression
    | ts.NonNullExpression
    | ts.PropertyAccessExpression;
  [AST_NODE_TYPES.ClassBody]: ts.ClassDeclaration | ts.ClassExpression;
  [AST_NODE_TYPES.ClassDeclaration]: ts.ClassDeclaration;
  [AST_NODE_TYPES.ClassExpression]: ts.ClassExpression;
  [AST_NODE_TYPES.ConditionalExpression]: ts.ConditionalExpression;
  [AST_NODE_TYPES.ContinueStatement]: ts.ContinueStatement;
  [AST_NODE_TYPES.DebuggerStatement]: ts.DebuggerStatement;
  [AST_NODE_TYPES.Decorator]: ts.Decorator;
  [AST_NODE_TYPES.DoWhileStatement]: ts.DoStatement;
  [AST_NODE_TYPES.EmptyStatement]: ts.EmptyStatement;
  [AST_NODE_TYPES.ExportAllDeclaration]: ts.ExportDeclaration;
  [AST_NODE_TYPES.ExportDefaultDeclaration]:
    | ts.ClassDeclaration
    | ts.ClassExpression
    | ts.EnumDeclaration
    | ts.ExportAssignment
    | ts.FunctionDeclaration
    | ts.InterfaceDeclaration
    | ts.ModuleDeclaration
    | ts.TypeAliasDeclaration
    | ts.VariableStatement;
  [AST_NODE_TYPES.ExportNamedDeclaration]:
    | ts.ClassDeclaration
    | ts.ClassExpression
    | ts.EnumDeclaration
    | ts.ExportDeclaration
    | ts.FunctionDeclaration
    | ts.ImportEqualsDeclaration
    | ts.InterfaceDeclaration
    | ts.ModuleDeclaration
    | ts.TypeAliasDeclaration
    | ts.VariableStatement;
  [AST_NODE_TYPES.ExportSpecifier]: ts.ExportSpecifier;
  [AST_NODE_TYPES.ExpressionStatement]: ts.ExpressionStatement;
  [AST_NODE_TYPES.ForInStatement]: ts.ForInStatement;
  [AST_NODE_TYPES.ForOfStatement]: ts.ForOfStatement;
  [AST_NODE_TYPES.ForStatement]: ts.ForStatement;
  [AST_NODE_TYPES.FunctionDeclaration]: ts.FunctionDeclaration;
  [AST_NODE_TYPES.FunctionExpression]:
    | ts.ConstructorDeclaration
    | ts.FunctionExpression
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration;
  [AST_NODE_TYPES.Identifier]:
    | ts.ConstructorDeclaration
    | ts.Identifier
    | ts.Token<ts.SyntaxKind.ImportKeyword | ts.SyntaxKind.NewKeyword>;
  [AST_NODE_TYPES.IfStatement]: ts.IfStatement;
  [AST_NODE_TYPES.PrivateIdentifier]: ts.PrivateIdentifier;
  [AST_NODE_TYPES.PropertyDefinition]: ts.PropertyDeclaration;
  // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
  [AST_NODE_TYPES.ImportAttribute]: 'ImportAttribute' extends keyof typeof ts
    ? ts.ImportAttribute
    : // eslint-disable-next-line @typescript-eslint/no-deprecated
      ts.AssertEntry;
  [AST_NODE_TYPES.ImportDeclaration]: ts.ImportDeclaration;
  [AST_NODE_TYPES.ImportDefaultSpecifier]: ts.ImportClause;
  [AST_NODE_TYPES.ImportExpression]: ts.CallExpression;
  [AST_NODE_TYPES.ImportNamespaceSpecifier]: ts.NamespaceImport;
  [AST_NODE_TYPES.ImportSpecifier]: ts.ImportSpecifier;
  [AST_NODE_TYPES.JSXAttribute]: ts.JsxAttribute;
  [AST_NODE_TYPES.JSXClosingElement]: ts.JsxClosingElement;
  [AST_NODE_TYPES.JSXClosingFragment]: ts.JsxClosingFragment;
  [AST_NODE_TYPES.JSXElement]: ts.JsxElement | ts.JsxSelfClosingElement;
  [AST_NODE_TYPES.JSXEmptyExpression]: ts.JsxExpression;
  [AST_NODE_TYPES.JSXExpressionContainer]: ts.JsxExpression;
  [AST_NODE_TYPES.JSXFragment]: ts.JsxFragment;
  [AST_NODE_TYPES.JSXIdentifier]: ts.Identifier | ts.ThisExpression;
  [AST_NODE_TYPES.JSXMemberExpression]: ts.PropertyAccessExpression;
  [AST_NODE_TYPES.JSXNamespacedName]: ts.JsxNamespacedName;
  [AST_NODE_TYPES.JSXOpeningElement]:
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement;
  [AST_NODE_TYPES.JSXOpeningFragment]: ts.JsxOpeningFragment;
  [AST_NODE_TYPES.JSXSpreadAttribute]: ts.JsxSpreadAttribute;
  [AST_NODE_TYPES.JSXSpreadChild]: ts.JsxExpression;
  [AST_NODE_TYPES.JSXText]: ts.JsxText;
  [AST_NODE_TYPES.LabeledStatement]: ts.LabeledStatement;
  [AST_NODE_TYPES.Literal]:
    | ts.BigIntLiteral
    | ts.BooleanLiteral
    | ts.NullLiteral
    | ts.NumericLiteral
    | ts.RegularExpressionLiteral
    | ts.StringLiteral;
  [AST_NODE_TYPES.LogicalExpression]: ts.BinaryExpression;
  [AST_NODE_TYPES.MemberExpression]:
    | ts.ElementAccessExpression
    | ts.PropertyAccessExpression;
  [AST_NODE_TYPES.MetaProperty]: ts.MetaProperty;
  [AST_NODE_TYPES.MethodDefinition]:
    | ts.ConstructorDeclaration
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration;
  [AST_NODE_TYPES.NewExpression]: ts.NewExpression;
  [AST_NODE_TYPES.ObjectExpression]: ts.ObjectLiteralExpression;
  [AST_NODE_TYPES.ObjectPattern]:
    | ts.ObjectBindingPattern
    | ts.ObjectLiteralExpression;
  [AST_NODE_TYPES.Program]: ts.SourceFile;
  [AST_NODE_TYPES.Property]:
    | ts.BindingElement
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.PropertyAssignment
    | ts.SetAccessorDeclaration
    | ts.ShorthandPropertyAssignment;
  [AST_NODE_TYPES.RestElement]:
    | ts.BindingElement
    | ts.ParameterDeclaration
    | ts.SpreadAssignment
    | ts.SpreadElement;
  [AST_NODE_TYPES.ReturnStatement]: ts.ReturnStatement;
  [AST_NODE_TYPES.SequenceExpression]: ts.BinaryExpression;
  [AST_NODE_TYPES.SpreadElement]: ts.SpreadAssignment | ts.SpreadElement;
  [AST_NODE_TYPES.StaticBlock]: ts.ClassStaticBlockDeclaration;
  [AST_NODE_TYPES.Super]: ts.SuperExpression;
  [AST_NODE_TYPES.SwitchCase]: ts.CaseClause | ts.DefaultClause;
  [AST_NODE_TYPES.SwitchStatement]: ts.SwitchStatement;
  [AST_NODE_TYPES.TaggedTemplateExpression]: ts.TaggedTemplateExpression;
  [AST_NODE_TYPES.TemplateElement]:
    | ts.NoSubstitutionTemplateLiteral
    | ts.TemplateHead
    | ts.TemplateMiddle
    | ts.TemplateTail;
  [AST_NODE_TYPES.TemplateLiteral]:
    | ts.NoSubstitutionTemplateLiteral
    | ts.TemplateExpression;
  [AST_NODE_TYPES.ThisExpression]:
    | ts.Identifier
    | ts.KeywordTypeNode
    | ts.ThisExpression;
  [AST_NODE_TYPES.ThrowStatement]: ts.ThrowStatement;
  [AST_NODE_TYPES.TryStatement]: ts.TryStatement;
  [AST_NODE_TYPES.TSAbstractAccessorProperty]: ts.PropertyDeclaration;
  [AST_NODE_TYPES.TSAbstractMethodDefinition]:
    | ts.ConstructorDeclaration
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration;
  [AST_NODE_TYPES.TSAbstractPropertyDefinition]: ts.PropertyDeclaration;
  [AST_NODE_TYPES.TSArrayType]: ts.ArrayTypeNode;
  [AST_NODE_TYPES.TSAsExpression]: ts.AsExpression;
  [AST_NODE_TYPES.TSCallSignatureDeclaration]: ts.CallSignatureDeclaration;
  [AST_NODE_TYPES.TSClassImplements]: ts.ExpressionWithTypeArguments;
  [AST_NODE_TYPES.TSConditionalType]: ts.ConditionalTypeNode;
  [AST_NODE_TYPES.TSConstructorType]: ts.ConstructorTypeNode;
  [AST_NODE_TYPES.TSConstructSignatureDeclaration]: ts.ConstructSignatureDeclaration;
  [AST_NODE_TYPES.TSDeclareFunction]: ts.FunctionDeclaration;
  [AST_NODE_TYPES.TSEnumBody]: ts.EnumDeclaration;
  [AST_NODE_TYPES.TSEnumDeclaration]: ts.EnumDeclaration;
  [AST_NODE_TYPES.TSEnumMember]: ts.EnumMember;
  [AST_NODE_TYPES.TSExportAssignment]: ts.ExportAssignment;
  [AST_NODE_TYPES.TSExternalModuleReference]: ts.ExternalModuleReference;
  [AST_NODE_TYPES.TSFunctionType]: ts.FunctionTypeNode;
  [AST_NODE_TYPES.TSImportEqualsDeclaration]: ts.ImportEqualsDeclaration;
  [AST_NODE_TYPES.TSImportType]: ts.ImportTypeNode;
  [AST_NODE_TYPES.TSIndexedAccessType]: ts.IndexedAccessTypeNode;
  [AST_NODE_TYPES.TSIndexSignature]: ts.IndexSignatureDeclaration;
  [AST_NODE_TYPES.TSInferType]: ts.InferTypeNode;
  [AST_NODE_TYPES.TSInstantiationExpression]: ts.ExpressionWithTypeArguments;
  [AST_NODE_TYPES.TSInterfaceBody]: ts.InterfaceDeclaration;
  [AST_NODE_TYPES.TSInterfaceDeclaration]: ts.InterfaceDeclaration;
  [AST_NODE_TYPES.TSInterfaceHeritage]: ts.ExpressionWithTypeArguments;
  [AST_NODE_TYPES.TSIntersectionType]: ts.IntersectionTypeNode;
  [AST_NODE_TYPES.TSLiteralType]: ts.LiteralTypeNode;
  [AST_NODE_TYPES.TSMappedType]: ts.MappedTypeNode;
  [AST_NODE_TYPES.TSMethodSignature]:
    | ts.GetAccessorDeclaration
    | ts.MethodSignature
    | ts.SetAccessorDeclaration;
  [AST_NODE_TYPES.TSModuleBlock]: ts.ModuleBlock;
  [AST_NODE_TYPES.TSModuleDeclaration]: ts.ModuleDeclaration;
  [AST_NODE_TYPES.TSNamedTupleMember]: ts.NamedTupleMember;
  [AST_NODE_TYPES.TSNamespaceExportDeclaration]: ts.NamespaceExportDeclaration;
  [AST_NODE_TYPES.TSNonNullExpression]: ts.NonNullExpression;
  [AST_NODE_TYPES.TSOptionalType]: ts.OptionalTypeNode;
  [AST_NODE_TYPES.TSParameterProperty]: ts.ParameterDeclaration;
  [AST_NODE_TYPES.TSPropertySignature]: ts.PropertySignature;
  [AST_NODE_TYPES.TSQualifiedName]: ts.Identifier | ts.QualifiedName;
  [AST_NODE_TYPES.TSRestType]:
    | ts.NamedTupleMember // for consistency and following babel's choices, a named tuple member with a rest gets converted to a TSRestType
    | ts.RestTypeNode;
  [AST_NODE_TYPES.TSSatisfiesExpression]: ts.SatisfiesExpression;
  [AST_NODE_TYPES.TSTemplateLiteralType]: ts.TemplateLiteralTypeNode;
  [AST_NODE_TYPES.TSThisType]: ts.ThisTypeNode;
  [AST_NODE_TYPES.TSTupleType]: ts.TupleTypeNode;
  [AST_NODE_TYPES.TSTypeAliasDeclaration]: ts.TypeAliasDeclaration;
  [AST_NODE_TYPES.TSTypeAnnotation]: undefined;
  [AST_NODE_TYPES.TSTypeAssertion]: ts.TypeAssertion;
  [AST_NODE_TYPES.TSTypeLiteral]: ts.TypeLiteralNode;
  [AST_NODE_TYPES.TSTypeOperator]: ts.TypeOperatorNode;
  [AST_NODE_TYPES.TSTypeParameter]: ts.TypeParameterDeclaration;
  [AST_NODE_TYPES.TSTypeParameterDeclaration]: undefined;
  [AST_NODE_TYPES.TSTypeParameterInstantiation]:
    | ts.CallExpression
    | ts.ExpressionWithTypeArguments
    | ts.ImportTypeNode
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement
    | ts.NewExpression
    | ts.TaggedTemplateExpression
    | ts.TypeQueryNode
    | ts.TypeReferenceNode;
  [AST_NODE_TYPES.TSTypePredicate]: ts.TypePredicateNode;
  [AST_NODE_TYPES.TSTypeQuery]: ts.ImportTypeNode | ts.TypeQueryNode;
  [AST_NODE_TYPES.TSTypeReference]: ts.TypeReferenceNode;
  [AST_NODE_TYPES.TSUnionType]: ts.UnionTypeNode;
  [AST_NODE_TYPES.UnaryExpression]:
    | ts.DeleteExpression
    | ts.PostfixUnaryExpression
    | ts.PrefixUnaryExpression
    | ts.TypeOfExpression
    | ts.VoidExpression;
  [AST_NODE_TYPES.UpdateExpression]:
    | ts.PostfixUnaryExpression
    | ts.PrefixUnaryExpression;
  [AST_NODE_TYPES.VariableDeclaration]:
    | ts.VariableDeclarationList
    | ts.VariableStatement;
  [AST_NODE_TYPES.VariableDeclarator]: ts.VariableDeclaration;
  [AST_NODE_TYPES.WhileStatement]: ts.WhileStatement;
  [AST_NODE_TYPES.WithStatement]: ts.WithStatement;
  [AST_NODE_TYPES.YieldExpression]: ts.YieldExpression;

  // Added by parser
  // Should be same as AST_NODE_TYPES.FunctionExpression
  [AST_NODE_TYPES.TSEmptyBodyFunctionExpression]:
    | ts.ConstructorDeclaration
    | ts.FunctionExpression
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration;

  // Keywords
  [AST_NODE_TYPES.TSAbstractKeyword]: ts.Token<ts.SyntaxKind.AbstractKeyword>;
  [AST_NODE_TYPES.TSAnyKeyword]: ts.KeywordTypeNode;

  [AST_NODE_TYPES.TSBigIntKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSBooleanKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSIntrinsicKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSNeverKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSNullKeyword]: ts.KeywordTypeNode | ts.NullLiteral;
  [AST_NODE_TYPES.TSNumberKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSObjectKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSStringKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSSymbolKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSUndefinedKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSUnknownKeyword]: ts.KeywordTypeNode;
  [AST_NODE_TYPES.TSVoidKeyword]: ts.KeywordTypeNode;

  // Unused
  [AST_NODE_TYPES.TSAsyncKeyword]: ts.Token<ts.SyntaxKind.AsyncKeyword>;
  [AST_NODE_TYPES.TSDeclareKeyword]: ts.Token<ts.SyntaxKind.DeclareKeyword>;
  [AST_NODE_TYPES.TSExportKeyword]: ts.Token<ts.SyntaxKind.ExportKeyword>;
  [AST_NODE_TYPES.TSPrivateKeyword]: ts.Token<ts.SyntaxKind.PrivateKeyword>;
  [AST_NODE_TYPES.TSProtectedKeyword]: ts.Token<ts.SyntaxKind.ProtectedKeyword>;
  [AST_NODE_TYPES.TSPublicKeyword]: ts.Token<ts.SyntaxKind.PublicKeyword>;
  [AST_NODE_TYPES.TSReadonlyKeyword]: ts.Token<ts.SyntaxKind.ReadonlyKeyword>;
  [AST_NODE_TYPES.TSStaticKeyword]: ts.Token<ts.SyntaxKind.StaticKeyword>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `[AST_NODE_TYPES.AccessorProperty]` | `ts.PropertyDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.ArrayExpression]` | `ts.ArrayLiteralExpression` | ✗ |  |
| `[AST_NODE_TYPES.ArrayPattern]` | `| ts.ArrayBindingPattern
    | ts.ArrayLiteralExpression` | ✗ |  |
| `[AST_NODE_TYPES.ArrowFunctionExpression]` | `ts.ArrowFunction` | ✗ |  |
| `[AST_NODE_TYPES.AssignmentExpression]` | `ts.BinaryExpression` | ✗ |  |
| `[AST_NODE_TYPES.AssignmentPattern]` | `| ts.BinaryExpression
    | ts.BindingElement
    | ts.ParameterDeclaration
    | ts.ShorthandPropertyAssignment` | ✗ |  |
| `[AST_NODE_TYPES.AwaitExpression]` | `ts.AwaitExpression` | ✗ |  |
| `[AST_NODE_TYPES.BinaryExpression]` | `ts.BinaryExpression` | ✗ |  |
| `[AST_NODE_TYPES.BlockStatement]` | `ts.Block` | ✗ |  |
| `[AST_NODE_TYPES.BreakStatement]` | `ts.BreakStatement` | ✗ |  |
| `[AST_NODE_TYPES.CallExpression]` | `ts.CallExpression` | ✗ |  |
| `[AST_NODE_TYPES.CatchClause]` | `ts.CatchClause` | ✗ |  |
| `[AST_NODE_TYPES.ChainExpression]` | `| ts.CallExpression
    | ts.ElementAccessExpression
    | ts.NonNullExpression
    | ts.PropertyAccessExpression` | ✗ |  |
| `[AST_NODE_TYPES.ClassBody]` | `ts.ClassDeclaration | ts.ClassExpression` | ✗ |  |
| `[AST_NODE_TYPES.ClassDeclaration]` | `ts.ClassDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.ClassExpression]` | `ts.ClassExpression` | ✗ |  |
| `[AST_NODE_TYPES.ConditionalExpression]` | `ts.ConditionalExpression` | ✗ |  |
| `[AST_NODE_TYPES.ContinueStatement]` | `ts.ContinueStatement` | ✗ |  |
| `[AST_NODE_TYPES.DebuggerStatement]` | `ts.DebuggerStatement` | ✗ |  |
| `[AST_NODE_TYPES.Decorator]` | `ts.Decorator` | ✗ |  |
| `[AST_NODE_TYPES.DoWhileStatement]` | `ts.DoStatement` | ✗ |  |
| `[AST_NODE_TYPES.EmptyStatement]` | `ts.EmptyStatement` | ✗ |  |
| `[AST_NODE_TYPES.ExportAllDeclaration]` | `ts.ExportDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.ExportDefaultDeclaration]` | `| ts.ClassDeclaration
    | ts.ClassExpression
    | ts.EnumDeclaration
    | ts.ExportAssignment
    | ts.FunctionDeclaration
    | ts.InterfaceDeclaration
    | ts.ModuleDeclaration
    | ts.TypeAliasDeclaration
    | ts.VariableStatement` | ✗ |  |
| `[AST_NODE_TYPES.ExportNamedDeclaration]` | `| ts.ClassDeclaration
    | ts.ClassExpression
    | ts.EnumDeclaration
    | ts.ExportDeclaration
    | ts.FunctionDeclaration
    | ts.ImportEqualsDeclaration
    | ts.InterfaceDeclaration
    | ts.ModuleDeclaration
    | ts.TypeAliasDeclaration
    | ts.VariableStatement` | ✗ |  |
| `[AST_NODE_TYPES.ExportSpecifier]` | `ts.ExportSpecifier` | ✗ |  |
| `[AST_NODE_TYPES.ExpressionStatement]` | `ts.ExpressionStatement` | ✗ |  |
| `[AST_NODE_TYPES.ForInStatement]` | `ts.ForInStatement` | ✗ |  |
| `[AST_NODE_TYPES.ForOfStatement]` | `ts.ForOfStatement` | ✗ |  |
| `[AST_NODE_TYPES.ForStatement]` | `ts.ForStatement` | ✗ |  |
| `[AST_NODE_TYPES.FunctionDeclaration]` | `ts.FunctionDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.FunctionExpression]` | `| ts.ConstructorDeclaration
    | ts.FunctionExpression
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.Identifier]` | `| ts.ConstructorDeclaration
    | ts.Identifier
    | ts.Token<ts.SyntaxKind.ImportKeyword | ts.SyntaxKind.NewKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.IfStatement]` | `ts.IfStatement` | ✗ |  |
| `[AST_NODE_TYPES.PrivateIdentifier]` | `ts.PrivateIdentifier` | ✗ |  |
| `[AST_NODE_TYPES.PropertyDefinition]` | `ts.PropertyDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.ImportAttribute]` | `'ImportAttribute' extends keyof typeof ts
    ? ts.ImportAttribute
    : // eslint-disable-next-line @typescript-eslint/no-deprecated
      ts.AssertEntry` | ✗ |  |
| `[AST_NODE_TYPES.ImportDeclaration]` | `ts.ImportDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.ImportDefaultSpecifier]` | `ts.ImportClause` | ✗ |  |
| `[AST_NODE_TYPES.ImportExpression]` | `ts.CallExpression` | ✗ |  |
| `[AST_NODE_TYPES.ImportNamespaceSpecifier]` | `ts.NamespaceImport` | ✗ |  |
| `[AST_NODE_TYPES.ImportSpecifier]` | `ts.ImportSpecifier` | ✗ |  |
| `[AST_NODE_TYPES.JSXAttribute]` | `ts.JsxAttribute` | ✗ |  |
| `[AST_NODE_TYPES.JSXClosingElement]` | `ts.JsxClosingElement` | ✗ |  |
| `[AST_NODE_TYPES.JSXClosingFragment]` | `ts.JsxClosingFragment` | ✗ |  |
| `[AST_NODE_TYPES.JSXElement]` | `ts.JsxElement | ts.JsxSelfClosingElement` | ✗ |  |
| `[AST_NODE_TYPES.JSXEmptyExpression]` | `ts.JsxExpression` | ✗ |  |
| `[AST_NODE_TYPES.JSXExpressionContainer]` | `ts.JsxExpression` | ✗ |  |
| `[AST_NODE_TYPES.JSXFragment]` | `ts.JsxFragment` | ✗ |  |
| `[AST_NODE_TYPES.JSXIdentifier]` | `ts.Identifier | ts.ThisExpression` | ✗ |  |
| `[AST_NODE_TYPES.JSXMemberExpression]` | `ts.PropertyAccessExpression` | ✗ |  |
| `[AST_NODE_TYPES.JSXNamespacedName]` | `ts.JsxNamespacedName` | ✗ |  |
| `[AST_NODE_TYPES.JSXOpeningElement]` | `| ts.JsxOpeningElement
    | ts.JsxSelfClosingElement` | ✗ |  |
| `[AST_NODE_TYPES.JSXOpeningFragment]` | `ts.JsxOpeningFragment` | ✗ |  |
| `[AST_NODE_TYPES.JSXSpreadAttribute]` | `ts.JsxSpreadAttribute` | ✗ |  |
| `[AST_NODE_TYPES.JSXSpreadChild]` | `ts.JsxExpression` | ✗ |  |
| `[AST_NODE_TYPES.JSXText]` | `ts.JsxText` | ✗ |  |
| `[AST_NODE_TYPES.LabeledStatement]` | `ts.LabeledStatement` | ✗ |  |
| `[AST_NODE_TYPES.Literal]` | `| ts.BigIntLiteral
    | ts.BooleanLiteral
    | ts.NullLiteral
    | ts.NumericLiteral
    | ts.RegularExpressionLiteral
    | ts.StringLiteral` | ✗ |  |
| `[AST_NODE_TYPES.LogicalExpression]` | `ts.BinaryExpression` | ✗ |  |
| `[AST_NODE_TYPES.MemberExpression]` | `| ts.ElementAccessExpression
    | ts.PropertyAccessExpression` | ✗ |  |
| `[AST_NODE_TYPES.MetaProperty]` | `ts.MetaProperty` | ✗ |  |
| `[AST_NODE_TYPES.MethodDefinition]` | `| ts.ConstructorDeclaration
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.NewExpression]` | `ts.NewExpression` | ✗ |  |
| `[AST_NODE_TYPES.ObjectExpression]` | `ts.ObjectLiteralExpression` | ✗ |  |
| `[AST_NODE_TYPES.ObjectPattern]` | `| ts.ObjectBindingPattern
    | ts.ObjectLiteralExpression` | ✗ |  |
| `[AST_NODE_TYPES.Program]` | `ts.SourceFile` | ✗ |  |
| `[AST_NODE_TYPES.Property]` | `| ts.BindingElement
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.PropertyAssignment
    | ts.SetAccessorDeclaration
    | ts.ShorthandPropertyAssignment` | ✗ |  |
| `[AST_NODE_TYPES.RestElement]` | `| ts.BindingElement
    | ts.ParameterDeclaration
    | ts.SpreadAssignment
    | ts.SpreadElement` | ✗ |  |
| `[AST_NODE_TYPES.ReturnStatement]` | `ts.ReturnStatement` | ✗ |  |
| `[AST_NODE_TYPES.SequenceExpression]` | `ts.BinaryExpression` | ✗ |  |
| `[AST_NODE_TYPES.SpreadElement]` | `ts.SpreadAssignment | ts.SpreadElement` | ✗ |  |
| `[AST_NODE_TYPES.StaticBlock]` | `ts.ClassStaticBlockDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.Super]` | `ts.SuperExpression` | ✗ |  |
| `[AST_NODE_TYPES.SwitchCase]` | `ts.CaseClause | ts.DefaultClause` | ✗ |  |
| `[AST_NODE_TYPES.SwitchStatement]` | `ts.SwitchStatement` | ✗ |  |
| `[AST_NODE_TYPES.TaggedTemplateExpression]` | `ts.TaggedTemplateExpression` | ✗ |  |
| `[AST_NODE_TYPES.TemplateElement]` | `| ts.NoSubstitutionTemplateLiteral
    | ts.TemplateHead
    | ts.TemplateMiddle
    | ts.TemplateTail` | ✗ |  |
| `[AST_NODE_TYPES.TemplateLiteral]` | `| ts.NoSubstitutionTemplateLiteral
    | ts.TemplateExpression` | ✗ |  |
| `[AST_NODE_TYPES.ThisExpression]` | `| ts.Identifier
    | ts.KeywordTypeNode
    | ts.ThisExpression` | ✗ |  |
| `[AST_NODE_TYPES.ThrowStatement]` | `ts.ThrowStatement` | ✗ |  |
| `[AST_NODE_TYPES.TryStatement]` | `ts.TryStatement` | ✗ |  |
| `[AST_NODE_TYPES.TSAbstractAccessorProperty]` | `ts.PropertyDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSAbstractMethodDefinition]` | `| ts.ConstructorDeclaration
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSAbstractPropertyDefinition]` | `ts.PropertyDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSArrayType]` | `ts.ArrayTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSAsExpression]` | `ts.AsExpression` | ✗ |  |
| `[AST_NODE_TYPES.TSCallSignatureDeclaration]` | `ts.CallSignatureDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSClassImplements]` | `ts.ExpressionWithTypeArguments` | ✗ |  |
| `[AST_NODE_TYPES.TSConditionalType]` | `ts.ConditionalTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSConstructorType]` | `ts.ConstructorTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSConstructSignatureDeclaration]` | `ts.ConstructSignatureDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSDeclareFunction]` | `ts.FunctionDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSEnumBody]` | `ts.EnumDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSEnumDeclaration]` | `ts.EnumDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSEnumMember]` | `ts.EnumMember` | ✗ |  |
| `[AST_NODE_TYPES.TSExportAssignment]` | `ts.ExportAssignment` | ✗ |  |
| `[AST_NODE_TYPES.TSExternalModuleReference]` | `ts.ExternalModuleReference` | ✗ |  |
| `[AST_NODE_TYPES.TSFunctionType]` | `ts.FunctionTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSImportEqualsDeclaration]` | `ts.ImportEqualsDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSImportType]` | `ts.ImportTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSIndexedAccessType]` | `ts.IndexedAccessTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSIndexSignature]` | `ts.IndexSignatureDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSInferType]` | `ts.InferTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSInstantiationExpression]` | `ts.ExpressionWithTypeArguments` | ✗ |  |
| `[AST_NODE_TYPES.TSInterfaceBody]` | `ts.InterfaceDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSInterfaceDeclaration]` | `ts.InterfaceDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSInterfaceHeritage]` | `ts.ExpressionWithTypeArguments` | ✗ |  |
| `[AST_NODE_TYPES.TSIntersectionType]` | `ts.IntersectionTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSLiteralType]` | `ts.LiteralTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSMappedType]` | `ts.MappedTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSMethodSignature]` | `| ts.GetAccessorDeclaration
    | ts.MethodSignature
    | ts.SetAccessorDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSModuleBlock]` | `ts.ModuleBlock` | ✗ |  |
| `[AST_NODE_TYPES.TSModuleDeclaration]` | `ts.ModuleDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSNamedTupleMember]` | `ts.NamedTupleMember` | ✗ |  |
| `[AST_NODE_TYPES.TSNamespaceExportDeclaration]` | `ts.NamespaceExportDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSNonNullExpression]` | `ts.NonNullExpression` | ✗ |  |
| `[AST_NODE_TYPES.TSOptionalType]` | `ts.OptionalTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSParameterProperty]` | `ts.ParameterDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSPropertySignature]` | `ts.PropertySignature` | ✗ |  |
| `[AST_NODE_TYPES.TSQualifiedName]` | `ts.Identifier | ts.QualifiedName` | ✗ |  |
| `[AST_NODE_TYPES.TSRestType]` | `| ts.NamedTupleMember // for consistency and following babel's choices, a named tuple member with a rest gets converted to a TSRestType
    | ts.RestTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSSatisfiesExpression]` | `ts.SatisfiesExpression` | ✗ |  |
| `[AST_NODE_TYPES.TSTemplateLiteralType]` | `ts.TemplateLiteralTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSThisType]` | `ts.ThisTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTupleType]` | `ts.TupleTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeAliasDeclaration]` | `ts.TypeAliasDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeAnnotation]` | `undefined` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeAssertion]` | `ts.TypeAssertion` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeLiteral]` | `ts.TypeLiteralNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeOperator]` | `ts.TypeOperatorNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeParameter]` | `ts.TypeParameterDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeParameterDeclaration]` | `undefined` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeParameterInstantiation]` | `| ts.CallExpression
    | ts.ExpressionWithTypeArguments
    | ts.ImportTypeNode
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement
    | ts.NewExpression
    | ts.TaggedTemplateExpression
    | ts.TypeQueryNode
    | ts.TypeReferenceNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypePredicate]` | `ts.TypePredicateNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeQuery]` | `ts.ImportTypeNode | ts.TypeQueryNode` | ✗ |  |
| `[AST_NODE_TYPES.TSTypeReference]` | `ts.TypeReferenceNode` | ✗ |  |
| `[AST_NODE_TYPES.TSUnionType]` | `ts.UnionTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.UnaryExpression]` | `| ts.DeleteExpression
    | ts.PostfixUnaryExpression
    | ts.PrefixUnaryExpression
    | ts.TypeOfExpression
    | ts.VoidExpression` | ✗ |  |
| `[AST_NODE_TYPES.UpdateExpression]` | `| ts.PostfixUnaryExpression
    | ts.PrefixUnaryExpression` | ✗ |  |
| `[AST_NODE_TYPES.VariableDeclaration]` | `| ts.VariableDeclarationList
    | ts.VariableStatement` | ✗ |  |
| `[AST_NODE_TYPES.VariableDeclarator]` | `ts.VariableDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.WhileStatement]` | `ts.WhileStatement` | ✗ |  |
| `[AST_NODE_TYPES.WithStatement]` | `ts.WithStatement` | ✗ |  |
| `[AST_NODE_TYPES.YieldExpression]` | `ts.YieldExpression` | ✗ |  |
| `[AST_NODE_TYPES.TSEmptyBodyFunctionExpression]` | `| ts.ConstructorDeclaration
    | ts.FunctionExpression
    | ts.GetAccessorDeclaration
    | ts.MethodDeclaration
    | ts.SetAccessorDeclaration` | ✗ |  |
| `[AST_NODE_TYPES.TSAbstractKeyword]` | `ts.Token<ts.SyntaxKind.AbstractKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSAnyKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSBigIntKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSBooleanKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSIntrinsicKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSNeverKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSNullKeyword]` | `ts.KeywordTypeNode | ts.NullLiteral` | ✗ |  |
| `[AST_NODE_TYPES.TSNumberKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSObjectKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSStringKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSSymbolKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSUndefinedKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSUnknownKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSVoidKeyword]` | `ts.KeywordTypeNode` | ✗ |  |
| `[AST_NODE_TYPES.TSAsyncKeyword]` | `ts.Token<ts.SyntaxKind.AsyncKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSDeclareKeyword]` | `ts.Token<ts.SyntaxKind.DeclareKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSExportKeyword]` | `ts.Token<ts.SyntaxKind.ExportKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSPrivateKeyword]` | `ts.Token<ts.SyntaxKind.PrivateKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSProtectedKeyword]` | `ts.Token<ts.SyntaxKind.ProtectedKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSPublicKeyword]` | `ts.Token<ts.SyntaxKind.PublicKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSReadonlyKeyword]` | `ts.Token<ts.SyntaxKind.ReadonlyKeyword>` | ✗ |  |
| `[AST_NODE_TYPES.TSStaticKeyword]` | `ts.Token<ts.SyntaxKind.StaticKeyword>` | ✗ |  |


---

## Type Aliases

### `TSESTreeToTSNode<T extends TSESTree.Node = TSESTree.Node extends TSESTree.Node = TSESTree.Node>`

/**
 * Maps TSESTree AST Node type to the expected TypeScript AST Node type(s).
 * This mapping is based on the internal logic of the parser.
 */

```ts
type TSESTreeToTSNode<T extends TSESTree.Node = TSESTree.Node extends TSESTree.Node = TSESTree.Node> = Extract<
  ts.Token<ts.SyntaxKind.ImportKeyword | ts.SyntaxKind.NewKeyword> | TSNode,
  // if this errors, it means that one of the AST_NODE_TYPES is not defined in the above interface
  EstreeToTsNodeTypes[T['type']]
>;
```


---