[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DeclarationStatement.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 13 |
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