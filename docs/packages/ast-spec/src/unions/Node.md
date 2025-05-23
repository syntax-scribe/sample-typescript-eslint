[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Node.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 168
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/Node.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ClassDeclaration` | `../declaration/ClassDeclaration/spec` |
| `ExportAllDeclaration` | `../declaration/ExportAllDeclaration/spec` |
| `ExportDefaultDeclaration` | `../declaration/ExportDefaultDeclaration/spec` |
| `ExportNamedDeclaration` | `../declaration/ExportNamedDeclaration/spec` |
| `FunctionDeclaration` | `../declaration/FunctionDeclaration/spec` |
| `ImportDeclaration` | `../declaration/ImportDeclaration/spec` |
| `TSDeclareFunction` | `../declaration/TSDeclareFunction/spec` |
| `TSEnumDeclaration` | `../declaration/TSEnumDeclaration/spec` |
| `TSImportEqualsDeclaration` | `../declaration/TSImportEqualsDeclaration/spec` |
| `TSInterfaceDeclaration` | `../declaration/TSInterfaceDeclaration/spec` |
| `TSModuleDeclaration` | `../declaration/TSModuleDeclaration/spec` |
| `TSNamespaceExportDeclaration` | `../declaration/TSNamespaceExportDeclaration/spec` |
| `TSTypeAliasDeclaration` | `../declaration/TSTypeAliasDeclaration/spec` |
| `VariableDeclaration` | `../declaration/VariableDeclaration/spec` |
| `AccessorProperty` | `../element/AccessorProperty/spec` |
| `MethodDefinition` | `../element/MethodDefinition/spec` |
| `Property` | `../element/Property/spec` |
| `PropertyDefinition` | `../element/PropertyDefinition/spec` |
| `SpreadElement` | `../element/SpreadElement/spec` |
| `StaticBlock` | `../element/StaticBlock/spec` |
| `TSAbstractAccessorProperty` | `../element/TSAbstractAccessorProperty/spec` |
| `TSAbstractMethodDefinition` | `../element/TSAbstractMethodDefinition/spec` |
| `TSAbstractPropertyDefinition` | `../element/TSAbstractPropertyDefinition/spec` |
| `TSCallSignatureDeclaration` | `../element/TSCallSignatureDeclaration/spec` |
| `TSConstructSignatureDeclaration` | `../element/TSConstructSignatureDeclaration/spec` |
| `TSEnumMember` | `../element/TSEnumMember/spec` |
| `TSIndexSignature` | `../element/TSIndexSignature/spec` |
| `TSMethodSignature` | `../element/TSMethodSignature/spec` |
| `TSPropertySignature` | `../element/TSPropertySignature/spec` |
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
| `TSEmptyBodyFunctionExpression` | `../expression/TSEmptyBodyFunctionExpression/spec` |
| `TSInstantiationExpression` | `../expression/TSInstantiationExpression/spec` |
| `TSNonNullExpression` | `../expression/TSNonNullExpression/spec` |
| `TSSatisfiesExpression` | `../expression/TSSatisfiesExpression/spec` |
| `TSTypeAssertion` | `../expression/TSTypeAssertion/spec` |
| `UnaryExpression` | `../expression/UnaryExpression/spec` |
| `UpdateExpression` | `../expression/UpdateExpression/spec` |
| `YieldExpression` | `../expression/YieldExpression/spec` |
| `JSXAttribute` | `../jsx/JSXAttribute/spec` |
| `JSXClosingElement` | `../jsx/JSXClosingElement/spec` |
| `JSXClosingFragment` | `../jsx/JSXClosingFragment/spec` |
| `JSXEmptyExpression` | `../jsx/JSXEmptyExpression/spec` |
| `JSXExpressionContainer` | `../jsx/JSXExpressionContainer/spec` |
| `JSXIdentifier` | `../jsx/JSXIdentifier/spec` |
| `JSXMemberExpression` | `../jsx/JSXMemberExpression/spec` |
| `JSXNamespacedName` | `../jsx/JSXNamespacedName/spec` |
| `JSXOpeningElement` | `../jsx/JSXOpeningElement/spec` |
| `JSXOpeningFragment` | `../jsx/JSXOpeningFragment/spec` |
| `JSXSpreadAttribute` | `../jsx/JSXSpreadAttribute/spec` |
| `JSXSpreadChild` | `../jsx/JSXSpreadChild/spec` |
| `JSXText` | `../jsx/JSXText/spec` |
| `ArrayPattern` | `../parameter/ArrayPattern/spec` |
| `AssignmentPattern` | `../parameter/AssignmentPattern/spec` |
| `ObjectPattern` | `../parameter/ObjectPattern/spec` |
| `RestElement` | `../parameter/RestElement/spec` |
| `TSParameterProperty` | `../parameter/TSParameterProperty/spec` |
| `CatchClause` | `../special/CatchClause/spec` |
| `ClassBody` | `../special/ClassBody/spec` |
| `Decorator` | `../special/Decorator/spec` |
| `EmptyStatement` | `../special/EmptyStatement/spec` |
| `ExportSpecifier` | `../special/ExportSpecifier/spec` |
| `ImportAttribute` | `../special/ImportAttribute/spec` |
| `ImportDefaultSpecifier` | `../special/ImportDefaultSpecifier/spec` |
| `ImportNamespaceSpecifier` | `../special/ImportNamespaceSpecifier/spec` |
| `ImportSpecifier` | `../special/ImportSpecifier/spec` |
| `PrivateIdentifier` | `../special/PrivateIdentifier/spec` |
| `Program` | `../special/Program/spec` |
| `SwitchCase` | `../special/SwitchCase/spec` |
| `TemplateElement` | `../special/TemplateElement/spec` |
| `TSClassImplements` | `../special/TSClassImplements/spec` |
| `TSEnumBody` | `../special/TSEnumBody/spec` |
| `TSExternalModuleReference` | `../special/TSExternalModuleReference/spec` |
| `TSInterfaceBody` | `../special/TSInterfaceBody/spec` |
| `TSInterfaceHeritage` | `../special/TSInterfaceHeritage/spec` |
| `TSModuleBlock` | `../special/TSModuleBlock/spec` |
| `TSTypeAnnotation` | `../special/TSTypeAnnotation/spec` |
| `TSTypeParameter` | `../special/TSTypeParameter/spec` |
| `TSTypeParameterDeclaration` | `../special/TSTypeParameterDeclaration/spec` |
| `TSTypeParameterInstantiation` | `../special/TSTypeParameterInstantiation/spec` |
| `VariableDeclarator` | `../special/VariableDeclarator/spec` |
| `BlockStatement` | `../statement/BlockStatement/spec` |
| `BreakStatement` | `../statement/BreakStatement/spec` |
| `ContinueStatement` | `../statement/ContinueStatement/spec` |
| `DebuggerStatement` | `../statement/DebuggerStatement/spec` |
| `DoWhileStatement` | `../statement/DoWhileStatement/spec` |
| `ExpressionStatement` | `../statement/ExpressionStatement/spec` |
| `ForInStatement` | `../statement/ForInStatement/spec` |
| `ForOfStatement` | `../statement/ForOfStatement/spec` |
| `ForStatement` | `../statement/ForStatement/spec` |
| `IfStatement` | `../statement/IfStatement/spec` |
| `LabeledStatement` | `../statement/LabeledStatement/spec` |
| `ReturnStatement` | `../statement/ReturnStatement/spec` |
| `SwitchStatement` | `../statement/SwitchStatement/spec` |
| `ThrowStatement` | `../statement/ThrowStatement/spec` |
| `TryStatement` | `../statement/TryStatement/spec` |
| `TSExportAssignment` | `../statement/TSExportAssignment/spec` |
| `WhileStatement` | `../statement/WhileStatement/spec` |
| `WithStatement` | `../statement/WithStatement/spec` |
| `TSAbstractKeyword` | `../type/TSAbstractKeyword/spec` |
| `TSAnyKeyword` | `../type/TSAnyKeyword/spec` |
| `TSArrayType` | `../type/TSArrayType/spec` |
| `TSAsyncKeyword` | `../type/TSAsyncKeyword/spec` |
| `TSBigIntKeyword` | `../type/TSBigIntKeyword/spec` |
| `TSBooleanKeyword` | `../type/TSBooleanKeyword/spec` |
| `TSConditionalType` | `../type/TSConditionalType/spec` |
| `TSConstructorType` | `../type/TSConstructorType/spec` |
| `TSDeclareKeyword` | `../type/TSDeclareKeyword/spec` |
| `TSExportKeyword` | `../type/TSExportKeyword/spec` |
| `TSFunctionType` | `../type/TSFunctionType/spec` |
| `TSImportType` | `../type/TSImportType/spec` |
| `TSIndexedAccessType` | `../type/TSIndexedAccessType/spec` |
| `TSInferType` | `../type/TSInferType/spec` |
| `TSIntersectionType` | `../type/TSIntersectionType/spec` |
| `TSIntrinsicKeyword` | `../type/TSIntrinsicKeyword/spec` |
| `TSLiteralType` | `../type/TSLiteralType/spec` |
| `TSMappedType` | `../type/TSMappedType/spec` |
| `TSNamedTupleMember` | `../type/TSNamedTupleMember/spec` |
| `TSNeverKeyword` | `../type/TSNeverKeyword/spec` |
| `TSNullKeyword` | `../type/TSNullKeyword/spec` |
| `TSNumberKeyword` | `../type/TSNumberKeyword/spec` |
| `TSObjectKeyword` | `../type/TSObjectKeyword/spec` |
| `TSOptionalType` | `../type/TSOptionalType/spec` |
| `TSPrivateKeyword` | `../type/TSPrivateKeyword/spec` |
| `TSProtectedKeyword` | `../type/TSProtectedKeyword/spec` |
| `TSPublicKeyword` | `../type/TSPublicKeyword/spec` |
| `TSQualifiedName` | `../type/TSQualifiedName/spec` |
| `TSReadonlyKeyword` | `../type/TSReadonlyKeyword/spec` |
| `TSRestType` | `../type/TSRestType/spec` |
| `TSStaticKeyword` | `../type/TSStaticKeyword/spec` |
| `TSStringKeyword` | `../type/TSStringKeyword/spec` |
| `TSSymbolKeyword` | `../type/TSSymbolKeyword/spec` |
| `TSTemplateLiteralType` | `../type/TSTemplateLiteralType/spec` |
| `TSThisType` | `../type/TSThisType/spec` |
| `TSTupleType` | `../type/TSTupleType/spec` |
| `TSTypeLiteral` | `../type/TSTypeLiteral/spec` |
| `TSTypeOperator` | `../type/TSTypeOperator/spec` |
| `TSTypePredicate` | `../type/TSTypePredicate/spec` |
| `TSTypeQuery` | `../type/TSTypeQuery/spec` |
| `TSTypeReference` | `../type/TSTypeReference/spec` |
| `TSUndefinedKeyword` | `../type/TSUndefinedKeyword/spec` |
| `TSUnionType` | `../type/TSUnionType/spec` |
| `TSUnknownKeyword` | `../type/TSUnknownKeyword/spec` |
| `TSVoidKeyword` | `../type/TSVoidKeyword/spec` |
| `Literal` | `./Literal` |


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

### `Node`

```ts
type Node = | AccessorProperty
  | ArrayExpression
  | ArrayPattern
  | ArrowFunctionExpression
  | AssignmentExpression
  | AssignmentPattern
  | AwaitExpression
  | BinaryExpression
  | BlockStatement
  | BreakStatement
  | CallExpression
  | CatchClause
  | ChainExpression
  | ClassBody
  | ClassDeclaration
  | ClassExpression
  | ConditionalExpression
  | ContinueStatement
  | DebuggerStatement
  | Decorator
  | DoWhileStatement
  | EmptyStatement
  | ExportAllDeclaration
  | ExportDefaultDeclaration
  | ExportNamedDeclaration
  | ExportSpecifier
  | ExpressionStatement
  | ForInStatement
  | ForOfStatement
  | ForStatement
  | FunctionDeclaration
  | FunctionExpression
  | Identifier
  | IfStatement
  | ImportAttribute
  | ImportDeclaration
  | ImportDefaultSpecifier
  | ImportExpression
  | ImportNamespaceSpecifier
  | ImportSpecifier
  | JSXAttribute
  | JSXClosingElement
  | JSXClosingFragment
  | JSXElement
  | JSXEmptyExpression
  | JSXExpressionContainer
  | JSXFragment
  | JSXIdentifier
  | JSXMemberExpression
  | JSXNamespacedName
  | JSXOpeningElement
  | JSXOpeningFragment
  | JSXSpreadAttribute
  | JSXSpreadChild
  | JSXText
  | LabeledStatement
  | Literal
  | LogicalExpression
  | MemberExpression
  | MetaProperty
  | MethodDefinition
  | NewExpression
  | ObjectExpression
  | ObjectPattern
  | PrivateIdentifier
  | Program
  | Property
  | PropertyDefinition
  | RestElement
  | ReturnStatement
  | SequenceExpression
  | SpreadElement
  | StaticBlock
  | Super
  | SwitchCase
  | SwitchStatement
  | TaggedTemplateExpression
  | TemplateElement
  | TemplateLiteral
  | ThisExpression
  | ThrowStatement
  | TryStatement
  | TSAbstractAccessorProperty
  | TSAbstractKeyword
  | TSAbstractMethodDefinition
  | TSAbstractPropertyDefinition
  | TSAnyKeyword
  | TSArrayType
  | TSAsExpression
  | TSAsyncKeyword
  | TSBigIntKeyword
  | TSBooleanKeyword
  | TSCallSignatureDeclaration
  | TSClassImplements
  | TSConditionalType
  | TSConstructorType
  | TSConstructSignatureDeclaration
  | TSDeclareFunction
  | TSDeclareKeyword
  | TSEmptyBodyFunctionExpression
  | TSEnumBody
  | TSEnumDeclaration
  | TSEnumMember
  | TSExportAssignment
  | TSExportKeyword
  | TSExternalModuleReference
  | TSFunctionType
  | TSImportEqualsDeclaration
  | TSImportType
  | TSIndexedAccessType
  | TSIndexSignature
  | TSInferType
  | TSInstantiationExpression
  | TSInterfaceBody
  | TSInterfaceDeclaration
  | TSInterfaceHeritage
  | TSIntersectionType
  | TSIntrinsicKeyword
  | TSLiteralType
  | TSMappedType
  | TSMethodSignature
  | TSModuleBlock
  | TSModuleDeclaration
  | TSNamedTupleMember
  | TSNamespaceExportDeclaration
  | TSNeverKeyword
  | TSNonNullExpression
  | TSNullKeyword
  | TSNumberKeyword
  | TSObjectKeyword
  | TSOptionalType
  | TSParameterProperty
  | TSPrivateKeyword
  | TSPropertySignature
  | TSProtectedKeyword
  | TSPublicKeyword
  | TSQualifiedName
  | TSReadonlyKeyword
  | TSRestType
  | TSSatisfiesExpression
  | TSStaticKeyword
  | TSStringKeyword
  | TSSymbolKeyword
  | TSTemplateLiteralType
  | TSThisType
  | TSTupleType
  | TSTypeAliasDeclaration
  | TSTypeAnnotation
  | TSTypeAssertion
  | TSTypeLiteral
  | TSTypeOperator
  | TSTypeParameter
  | TSTypeParameterDeclaration
  | TSTypeParameterInstantiation
  | TSTypePredicate
  | TSTypeQuery
  | TSTypeReference
  | TSUndefinedKeyword
  | TSUnionType
  | TSUnknownKeyword
  | TSVoidKeyword
  | UnaryExpression
  | UpdateExpression
  | VariableDeclaration
  | VariableDeclarator
  | WhileStatement
  | WithStatement
  | YieldExpression;
```


---