[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ast-node-types.ts`

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
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 1 |

## 📚 Table of Contents

- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/ast-node-types.ts`**

## 🔧 Functions

> No functions found in this file.


---

## Enums

### `enum AST_NODE_TYPES`

<details><summary>Enum Code</summary>

```ts
export enum AST_NODE_TYPES {
  AccessorProperty = 'AccessorProperty',
  ArrayExpression = 'ArrayExpression',
  ArrayPattern = 'ArrayPattern',
  ArrowFunctionExpression = 'ArrowFunctionExpression',
  AssignmentExpression = 'AssignmentExpression',
  AssignmentPattern = 'AssignmentPattern',
  AwaitExpression = 'AwaitExpression',
  BinaryExpression = 'BinaryExpression',
  BlockStatement = 'BlockStatement',
  BreakStatement = 'BreakStatement',
  CallExpression = 'CallExpression',
  CatchClause = 'CatchClause',
  ChainExpression = 'ChainExpression',
  ClassBody = 'ClassBody',
  ClassDeclaration = 'ClassDeclaration',
  ClassExpression = 'ClassExpression',
  ConditionalExpression = 'ConditionalExpression',
  ContinueStatement = 'ContinueStatement',
  DebuggerStatement = 'DebuggerStatement',
  Decorator = 'Decorator',
  DoWhileStatement = 'DoWhileStatement',
  EmptyStatement = 'EmptyStatement',
  ExportAllDeclaration = 'ExportAllDeclaration',
  ExportDefaultDeclaration = 'ExportDefaultDeclaration',
  ExportNamedDeclaration = 'ExportNamedDeclaration',
  ExportSpecifier = 'ExportSpecifier',
  ExpressionStatement = 'ExpressionStatement',
  ForInStatement = 'ForInStatement',
  ForOfStatement = 'ForOfStatement',
  ForStatement = 'ForStatement',
  FunctionDeclaration = 'FunctionDeclaration',
  FunctionExpression = 'FunctionExpression',
  Identifier = 'Identifier',
  IfStatement = 'IfStatement',
  ImportAttribute = 'ImportAttribute',
  ImportDeclaration = 'ImportDeclaration',
  ImportDefaultSpecifier = 'ImportDefaultSpecifier',
  ImportExpression = 'ImportExpression',
  ImportNamespaceSpecifier = 'ImportNamespaceSpecifier',
  ImportSpecifier = 'ImportSpecifier',
  JSXAttribute = 'JSXAttribute',
  JSXClosingElement = 'JSXClosingElement',
  JSXClosingFragment = 'JSXClosingFragment',
  JSXElement = 'JSXElement',
  JSXEmptyExpression = 'JSXEmptyExpression',
  JSXExpressionContainer = 'JSXExpressionContainer',
  JSXFragment = 'JSXFragment',
  JSXIdentifier = 'JSXIdentifier',
  JSXMemberExpression = 'JSXMemberExpression',
  JSXNamespacedName = 'JSXNamespacedName',
  JSXOpeningElement = 'JSXOpeningElement',
  JSXOpeningFragment = 'JSXOpeningFragment',
  JSXSpreadAttribute = 'JSXSpreadAttribute',
  JSXSpreadChild = 'JSXSpreadChild',
  JSXText = 'JSXText',
  LabeledStatement = 'LabeledStatement',
  Literal = 'Literal',
  LogicalExpression = 'LogicalExpression',
  MemberExpression = 'MemberExpression',
  MetaProperty = 'MetaProperty',
  MethodDefinition = 'MethodDefinition',
  NewExpression = 'NewExpression',
  ObjectExpression = 'ObjectExpression',
  ObjectPattern = 'ObjectPattern',
  PrivateIdentifier = 'PrivateIdentifier',
  Program = 'Program',
  Property = 'Property',
  PropertyDefinition = 'PropertyDefinition',
  RestElement = 'RestElement',
  ReturnStatement = 'ReturnStatement',
  SequenceExpression = 'SequenceExpression',
  SpreadElement = 'SpreadElement',
  StaticBlock = 'StaticBlock',
  Super = 'Super',
  SwitchCase = 'SwitchCase',
  SwitchStatement = 'SwitchStatement',
  TaggedTemplateExpression = 'TaggedTemplateExpression',
  TemplateElement = 'TemplateElement',
  TemplateLiteral = 'TemplateLiteral',
  ThisExpression = 'ThisExpression',
  ThrowStatement = 'ThrowStatement',
  TryStatement = 'TryStatement',
  UnaryExpression = 'UnaryExpression',
  UpdateExpression = 'UpdateExpression',
  VariableDeclaration = 'VariableDeclaration',
  VariableDeclarator = 'VariableDeclarator',
  WhileStatement = 'WhileStatement',
  WithStatement = 'WithStatement',
  YieldExpression = 'YieldExpression',

  // TS_prefixed nodes
  TSAbstractAccessorProperty = 'TSAbstractAccessorProperty',
  TSAbstractKeyword = 'TSAbstractKeyword',
  TSAbstractMethodDefinition = 'TSAbstractMethodDefinition',
  TSAbstractPropertyDefinition = 'TSAbstractPropertyDefinition',
  TSAnyKeyword = 'TSAnyKeyword',
  TSArrayType = 'TSArrayType',
  TSAsExpression = 'TSAsExpression',
  TSAsyncKeyword = 'TSAsyncKeyword',
  TSBigIntKeyword = 'TSBigIntKeyword',
  TSBooleanKeyword = 'TSBooleanKeyword',
  TSCallSignatureDeclaration = 'TSCallSignatureDeclaration',
  TSClassImplements = 'TSClassImplements',
  TSConditionalType = 'TSConditionalType',
  TSConstructorType = 'TSConstructorType',
  TSConstructSignatureDeclaration = 'TSConstructSignatureDeclaration',
  TSDeclareFunction = 'TSDeclareFunction',
  TSDeclareKeyword = 'TSDeclareKeyword',
  TSEmptyBodyFunctionExpression = 'TSEmptyBodyFunctionExpression',
  TSEnumBody = 'TSEnumBody',
  TSEnumDeclaration = 'TSEnumDeclaration',
  TSEnumMember = 'TSEnumMember',
  TSExportAssignment = 'TSExportAssignment',
  TSExportKeyword = 'TSExportKeyword',
  TSExternalModuleReference = 'TSExternalModuleReference',
  TSFunctionType = 'TSFunctionType',
  TSImportEqualsDeclaration = 'TSImportEqualsDeclaration',
  TSImportType = 'TSImportType',
  TSIndexedAccessType = 'TSIndexedAccessType',
  TSIndexSignature = 'TSIndexSignature',
  TSInferType = 'TSInferType',
  TSInstantiationExpression = 'TSInstantiationExpression',
  TSInterfaceBody = 'TSInterfaceBody',
  TSInterfaceDeclaration = 'TSInterfaceDeclaration',
  TSInterfaceHeritage = 'TSInterfaceHeritage',
  TSIntersectionType = 'TSIntersectionType',
  TSIntrinsicKeyword = 'TSIntrinsicKeyword',
  TSLiteralType = 'TSLiteralType',
  TSMappedType = 'TSMappedType',
  TSMethodSignature = 'TSMethodSignature',
  TSModuleBlock = 'TSModuleBlock',
  TSModuleDeclaration = 'TSModuleDeclaration',
  TSNamedTupleMember = 'TSNamedTupleMember',
  TSNamespaceExportDeclaration = 'TSNamespaceExportDeclaration',
  TSNeverKeyword = 'TSNeverKeyword',
  TSNonNullExpression = 'TSNonNullExpression',
  TSNullKeyword = 'TSNullKeyword',
  TSNumberKeyword = 'TSNumberKeyword',
  TSObjectKeyword = 'TSObjectKeyword',
  TSOptionalType = 'TSOptionalType',
  TSParameterProperty = 'TSParameterProperty',
  TSPrivateKeyword = 'TSPrivateKeyword',
  TSPropertySignature = 'TSPropertySignature',
  TSProtectedKeyword = 'TSProtectedKeyword',
  TSPublicKeyword = 'TSPublicKeyword',
  TSQualifiedName = 'TSQualifiedName',
  TSReadonlyKeyword = 'TSReadonlyKeyword',
  TSRestType = 'TSRestType',
  TSSatisfiesExpression = 'TSSatisfiesExpression',
  TSStaticKeyword = 'TSStaticKeyword',
  TSStringKeyword = 'TSStringKeyword',
  TSSymbolKeyword = 'TSSymbolKeyword',
  TSTemplateLiteralType = 'TSTemplateLiteralType',
  TSThisType = 'TSThisType',
  TSTupleType = 'TSTupleType',
  TSTypeAliasDeclaration = 'TSTypeAliasDeclaration',
  TSTypeAnnotation = 'TSTypeAnnotation',
  TSTypeAssertion = 'TSTypeAssertion',
  TSTypeLiteral = 'TSTypeLiteral',
  TSTypeOperator = 'TSTypeOperator',
  TSTypeParameter = 'TSTypeParameter',
  TSTypeParameterDeclaration = 'TSTypeParameterDeclaration',
  TSTypeParameterInstantiation = 'TSTypeParameterInstantiation',
  TSTypePredicate = 'TSTypePredicate',
  TSTypeQuery = 'TSTypeQuery',
  TSTypeReference = 'TSTypeReference',
  TSUndefinedKeyword = 'TSUndefinedKeyword',
  TSUnionType = 'TSUnionType',
  TSUnknownKeyword = 'TSUnknownKeyword',
  TSVoidKeyword = 'TSVoidKeyword',
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `AccessorProperty` | `AccessorProperty` |  |
| `ArrayExpression` | `ArrayExpression` |  |
| `ArrayPattern` | `ArrayPattern` |  |
| `ArrowFunctionExpression` | `ArrowFunctionExpression` |  |
| `AssignmentExpression` | `AssignmentExpression` |  |
| `AssignmentPattern` | `AssignmentPattern` |  |
| `AwaitExpression` | `AwaitExpression` |  |
| `BinaryExpression` | `BinaryExpression` |  |
| `BlockStatement` | `BlockStatement` |  |
| `BreakStatement` | `BreakStatement` |  |
| `CallExpression` | `CallExpression` |  |
| `CatchClause` | `CatchClause` |  |
| `ChainExpression` | `ChainExpression` |  |
| `ClassBody` | `ClassBody` |  |
| `ClassDeclaration` | `ClassDeclaration` |  |
| `ClassExpression` | `ClassExpression` |  |
| `ConditionalExpression` | `ConditionalExpression` |  |
| `ContinueStatement` | `ContinueStatement` |  |
| `DebuggerStatement` | `DebuggerStatement` |  |
| `Decorator` | `Decorator` |  |
| `DoWhileStatement` | `DoWhileStatement` |  |
| `EmptyStatement` | `EmptyStatement` |  |
| `ExportAllDeclaration` | `ExportAllDeclaration` |  |
| `ExportDefaultDeclaration` | `ExportDefaultDeclaration` |  |
| `ExportNamedDeclaration` | `ExportNamedDeclaration` |  |
| `ExportSpecifier` | `ExportSpecifier` |  |
| `ExpressionStatement` | `ExpressionStatement` |  |
| `ForInStatement` | `ForInStatement` |  |
| `ForOfStatement` | `ForOfStatement` |  |
| `ForStatement` | `ForStatement` |  |
| `FunctionDeclaration` | `FunctionDeclaration` |  |
| `FunctionExpression` | `FunctionExpression` |  |
| `Identifier` | `Identifier` |  |
| `IfStatement` | `IfStatement` |  |
| `ImportAttribute` | `ImportAttribute` |  |
| `ImportDeclaration` | `ImportDeclaration` |  |
| `ImportDefaultSpecifier` | `ImportDefaultSpecifier` |  |
| `ImportExpression` | `ImportExpression` |  |
| `ImportNamespaceSpecifier` | `ImportNamespaceSpecifier` |  |
| `ImportSpecifier` | `ImportSpecifier` |  |
| `JSXAttribute` | `JSXAttribute` |  |
| `JSXClosingElement` | `JSXClosingElement` |  |
| `JSXClosingFragment` | `JSXClosingFragment` |  |
| `JSXElement` | `JSXElement` |  |
| `JSXEmptyExpression` | `JSXEmptyExpression` |  |
| `JSXExpressionContainer` | `JSXExpressionContainer` |  |
| `JSXFragment` | `JSXFragment` |  |
| `JSXIdentifier` | `JSXIdentifier` |  |
| `JSXMemberExpression` | `JSXMemberExpression` |  |
| `JSXNamespacedName` | `JSXNamespacedName` |  |
| `JSXOpeningElement` | `JSXOpeningElement` |  |
| `JSXOpeningFragment` | `JSXOpeningFragment` |  |
| `JSXSpreadAttribute` | `JSXSpreadAttribute` |  |
| `JSXSpreadChild` | `JSXSpreadChild` |  |
| `JSXText` | `JSXText` |  |
| `LabeledStatement` | `LabeledStatement` |  |
| `Literal` | `Literal` |  |
| `LogicalExpression` | `LogicalExpression` |  |
| `MemberExpression` | `MemberExpression` |  |
| `MetaProperty` | `MetaProperty` |  |
| `MethodDefinition` | `MethodDefinition` |  |
| `NewExpression` | `NewExpression` |  |
| `ObjectExpression` | `ObjectExpression` |  |
| `ObjectPattern` | `ObjectPattern` |  |
| `PrivateIdentifier` | `PrivateIdentifier` |  |
| `Program` | `Program` |  |
| `Property` | `Property` |  |
| `PropertyDefinition` | `PropertyDefinition` |  |
| `RestElement` | `RestElement` |  |
| `ReturnStatement` | `ReturnStatement` |  |
| `SequenceExpression` | `SequenceExpression` |  |
| `SpreadElement` | `SpreadElement` |  |
| `StaticBlock` | `StaticBlock` |  |
| `Super` | `Super` |  |
| `SwitchCase` | `SwitchCase` |  |
| `SwitchStatement` | `SwitchStatement` |  |
| `TaggedTemplateExpression` | `TaggedTemplateExpression` |  |
| `TemplateElement` | `TemplateElement` |  |
| `TemplateLiteral` | `TemplateLiteral` |  |
| `ThisExpression` | `ThisExpression` |  |
| `ThrowStatement` | `ThrowStatement` |  |
| `TryStatement` | `TryStatement` |  |
| `UnaryExpression` | `UnaryExpression` |  |
| `UpdateExpression` | `UpdateExpression` |  |
| `VariableDeclaration` | `VariableDeclaration` |  |
| `VariableDeclarator` | `VariableDeclarator` |  |
| `WhileStatement` | `WhileStatement` |  |
| `WithStatement` | `WithStatement` |  |
| `YieldExpression` | `YieldExpression` |  |
| `TSAbstractAccessorProperty` | `TSAbstractAccessorProperty` |  |
| `TSAbstractKeyword` | `TSAbstractKeyword` |  |
| `TSAbstractMethodDefinition` | `TSAbstractMethodDefinition` |  |
| `TSAbstractPropertyDefinition` | `TSAbstractPropertyDefinition` |  |
| `TSAnyKeyword` | `TSAnyKeyword` |  |
| `TSArrayType` | `TSArrayType` |  |
| `TSAsExpression` | `TSAsExpression` |  |
| `TSAsyncKeyword` | `TSAsyncKeyword` |  |
| `TSBigIntKeyword` | `TSBigIntKeyword` |  |
| `TSBooleanKeyword` | `TSBooleanKeyword` |  |
| `TSCallSignatureDeclaration` | `TSCallSignatureDeclaration` |  |
| `TSClassImplements` | `TSClassImplements` |  |
| `TSConditionalType` | `TSConditionalType` |  |
| `TSConstructorType` | `TSConstructorType` |  |
| `TSConstructSignatureDeclaration` | `TSConstructSignatureDeclaration` |  |
| `TSDeclareFunction` | `TSDeclareFunction` |  |
| `TSDeclareKeyword` | `TSDeclareKeyword` |  |
| `TSEmptyBodyFunctionExpression` | `TSEmptyBodyFunctionExpression` |  |
| `TSEnumBody` | `TSEnumBody` |  |
| `TSEnumDeclaration` | `TSEnumDeclaration` |  |
| `TSEnumMember` | `TSEnumMember` |  |
| `TSExportAssignment` | `TSExportAssignment` |  |
| `TSExportKeyword` | `TSExportKeyword` |  |
| `TSExternalModuleReference` | `TSExternalModuleReference` |  |
| `TSFunctionType` | `TSFunctionType` |  |
| `TSImportEqualsDeclaration` | `TSImportEqualsDeclaration` |  |
| `TSImportType` | `TSImportType` |  |
| `TSIndexedAccessType` | `TSIndexedAccessType` |  |
| `TSIndexSignature` | `TSIndexSignature` |  |
| `TSInferType` | `TSInferType` |  |
| `TSInstantiationExpression` | `TSInstantiationExpression` |  |
| `TSInterfaceBody` | `TSInterfaceBody` |  |
| `TSInterfaceDeclaration` | `TSInterfaceDeclaration` |  |
| `TSInterfaceHeritage` | `TSInterfaceHeritage` |  |
| `TSIntersectionType` | `TSIntersectionType` |  |
| `TSIntrinsicKeyword` | `TSIntrinsicKeyword` |  |
| `TSLiteralType` | `TSLiteralType` |  |
| `TSMappedType` | `TSMappedType` |  |
| `TSMethodSignature` | `TSMethodSignature` |  |
| `TSModuleBlock` | `TSModuleBlock` |  |
| `TSModuleDeclaration` | `TSModuleDeclaration` |  |
| `TSNamedTupleMember` | `TSNamedTupleMember` |  |
| `TSNamespaceExportDeclaration` | `TSNamespaceExportDeclaration` |  |
| `TSNeverKeyword` | `TSNeverKeyword` |  |
| `TSNonNullExpression` | `TSNonNullExpression` |  |
| `TSNullKeyword` | `TSNullKeyword` |  |
| `TSNumberKeyword` | `TSNumberKeyword` |  |
| `TSObjectKeyword` | `TSObjectKeyword` |  |
| `TSOptionalType` | `TSOptionalType` |  |
| `TSParameterProperty` | `TSParameterProperty` |  |
| `TSPrivateKeyword` | `TSPrivateKeyword` |  |
| `TSPropertySignature` | `TSPropertySignature` |  |
| `TSProtectedKeyword` | `TSProtectedKeyword` |  |
| `TSPublicKeyword` | `TSPublicKeyword` |  |
| `TSQualifiedName` | `TSQualifiedName` |  |
| `TSReadonlyKeyword` | `TSReadonlyKeyword` |  |
| `TSRestType` | `TSRestType` |  |
| `TSSatisfiesExpression` | `TSSatisfiesExpression` |  |
| `TSStaticKeyword` | `TSStaticKeyword` |  |
| `TSStringKeyword` | `TSStringKeyword` |  |
| `TSSymbolKeyword` | `TSSymbolKeyword` |  |
| `TSTemplateLiteralType` | `TSTemplateLiteralType` |  |
| `TSThisType` | `TSThisType` |  |
| `TSTupleType` | `TSTupleType` |  |
| `TSTypeAliasDeclaration` | `TSTypeAliasDeclaration` |  |
| `TSTypeAnnotation` | `TSTypeAnnotation` |  |
| `TSTypeAssertion` | `TSTypeAssertion` |  |
| `TSTypeLiteral` | `TSTypeLiteral` |  |
| `TSTypeOperator` | `TSTypeOperator` |  |
| `TSTypeParameter` | `TSTypeParameter` |  |
| `TSTypeParameterDeclaration` | `TSTypeParameterDeclaration` |  |
| `TSTypeParameterInstantiation` | `TSTypeParameterInstantiation` |  |
| `TSTypePredicate` | `TSTypePredicate` |  |
| `TSTypeQuery` | `TSTypeQuery` |  |
| `TSTypeReference` | `TSTypeReference` |  |
| `TSUndefinedKeyword` | `TSUndefinedKeyword` |  |
| `TSUnionType` | `TSUnionType` |  |
| `TSUnknownKeyword` | `TSUnknownKeyword` |  |
| `TSVoidKeyword` | `TSVoidKeyword` |  |


---