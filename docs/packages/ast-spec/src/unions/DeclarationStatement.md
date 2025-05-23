[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DeclarationStatement.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 13
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/DeclarationStatement.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ClassDeclaration` | `../declaration/ClassDeclaration/spec` |
| `ExportAllDeclaration` | `../declaration/ExportAllDeclaration/spec` |
| `ExportDefaultDeclaration` | `../declaration/ExportDefaultDeclaration/spec` |
| `ExportNamedDeclaration` | `../declaration/ExportNamedDeclaration/spec` |
| `FunctionDeclaration` | `../declaration/FunctionDeclaration/spec` |
| `TSDeclareFunction` | `../declaration/TSDeclareFunction/spec` |
| `TSEnumDeclaration` | `../declaration/TSEnumDeclaration/spec` |
| `TSImportEqualsDeclaration` | `../declaration/TSImportEqualsDeclaration/spec` |
| `TSInterfaceDeclaration` | `../declaration/TSInterfaceDeclaration/spec` |
| `TSModuleDeclaration` | `../declaration/TSModuleDeclaration/spec` |
| `TSNamespaceExportDeclaration` | `../declaration/TSNamespaceExportDeclaration/spec` |
| `TSTypeAliasDeclaration` | `../declaration/TSTypeAliasDeclaration/spec` |
| `ClassExpression` | `../expression/ClassExpression/spec` |


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

### `DeclarationStatement`

/**
 * @deprecated
 * Note that this is neither up to date nor fully correct.
 */

```ts
type DeclarationStatement = | ClassDeclaration
  | ClassExpression
  | ExportAllDeclaration
  | ExportDefaultDeclaration
  | ExportNamedDeclaration
  | FunctionDeclaration
  | TSDeclareFunction
  | TSEnumDeclaration
  | TSImportEqualsDeclaration
  | TSInterfaceDeclaration
  | TSModuleDeclaration
  | TSNamespaceExportDeclaration
  | TSTypeAliasDeclaration;
```


---