[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ExportDeclaration.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 12 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/unions/ExportDeclaration.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ClassDeclarationWithName` | `../declaration/ClassDeclaration/spec` |
| `ClassDeclarationWithOptionalName` | `../declaration/ClassDeclaration/spec` |
| `FunctionDeclarationWithName` | `../declaration/FunctionDeclaration/spec` |
| `FunctionDeclarationWithOptionalName` | `../declaration/FunctionDeclaration/spec` |
| `TSDeclareFunction` | `../declaration/TSDeclareFunction/spec` |
| `TSEnumDeclaration` | `../declaration/TSEnumDeclaration/spec` |
| `TSImportEqualsDeclaration` | `../declaration/TSImportEqualsDeclaration/spec` |
| `TSInterfaceDeclaration` | `../declaration/TSInterfaceDeclaration/spec` |
| `TSModuleDeclaration` | `../declaration/TSModuleDeclaration/spec` |
| `TSTypeAliasDeclaration` | `../declaration/TSTypeAliasDeclaration/spec` |
| `VariableDeclaration` | `../declaration/VariableDeclaration/spec` |
| `Expression` | `./Expression` |


---

## Type Aliases

### `DefaultExportDeclarations`

```ts
type DefaultExportDeclarations = | ClassDeclarationWithOptionalName
  | Expression
  | FunctionDeclarationWithName
  | FunctionDeclarationWithOptionalName
  | TSDeclareFunction
  | TSEnumDeclaration
  | TSInterfaceDeclaration
  | TSModuleDeclaration
  | TSTypeAliasDeclaration
  | VariableDeclaration;
```

### `NamedExportDeclarations`

```ts
type NamedExportDeclarations = | ClassDeclarationWithName
  | ClassDeclarationWithOptionalName
  | FunctionDeclarationWithName
  | FunctionDeclarationWithOptionalName
  | TSDeclareFunction
  | TSEnumDeclaration
  | TSImportEqualsDeclaration
  | TSInterfaceDeclaration
  | TSModuleDeclaration
  | TSTypeAliasDeclaration
  | VariableDeclaration;
```

### `ExportDeclaration`

```ts
type ExportDeclaration = | DefaultExportDeclarations
  | NamedExportDeclarations;
```


---