[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Statement.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 33
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/Statement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ClassDeclarationWithName` | `../declaration/ClassDeclaration/spec` |
| `ExportAllDeclaration` | `../declaration/ExportAllDeclaration/spec` |
| `ExportDefaultDeclaration` | `../declaration/ExportDefaultDeclaration/spec` |
| `ExportNamedDeclaration` | `../declaration/ExportNamedDeclaration/spec` |
| `FunctionDeclarationWithName` | `../declaration/FunctionDeclaration/spec` |
| `ImportDeclaration` | `../declaration/ImportDeclaration/spec` |
| `TSDeclareFunction` | `../declaration/TSDeclareFunction/spec` |
| `TSEnumDeclaration` | `../declaration/TSEnumDeclaration/spec` |
| `TSImportEqualsDeclaration` | `../declaration/TSImportEqualsDeclaration/spec` |
| `TSInterfaceDeclaration` | `../declaration/TSInterfaceDeclaration/spec` |
| `TSModuleDeclaration` | `../declaration/TSModuleDeclaration/spec` |
| `TSNamespaceExportDeclaration` | `../declaration/TSNamespaceExportDeclaration/spec` |
| `TSTypeAliasDeclaration` | `../declaration/TSTypeAliasDeclaration/spec` |
| `VariableDeclaration` | `../declaration/VariableDeclaration/spec` |
| `EmptyStatement` | `../special/EmptyStatement/spec` |
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

### `Statement`

```ts
type Statement = | BlockStatement
  | BreakStatement
  | ClassDeclarationWithName
  | ContinueStatement
  | DebuggerStatement
  | DoWhileStatement
  | EmptyStatement
  | ExportAllDeclaration
  | ExportDefaultDeclaration
  | ExportNamedDeclaration
  | ExpressionStatement
  | ForInStatement
  | ForOfStatement
  | ForStatement
  | FunctionDeclarationWithName
  | IfStatement
  | ImportDeclaration
  | LabeledStatement
  | ReturnStatement
  | SwitchStatement
  | ThrowStatement
  | TryStatement
  | TSDeclareFunction
  | TSEnumDeclaration
  | TSExportAssignment
  | TSImportEqualsDeclaration
  | TSInterfaceDeclaration
  | TSModuleDeclaration
  | TSNamespaceExportDeclaration
  | TSTypeAliasDeclaration
  | VariableDeclaration
  | WhileStatement
  | WithStatement;
```

### `ProgramStatement`

```ts
type ProgramStatement = | ExportAllDeclaration
  | ExportDefaultDeclaration
  | ExportNamedDeclaration
  | ImportDeclaration
  | Statement
  | TSImportEqualsDeclaration
  | TSNamespaceExportDeclaration;
```


---