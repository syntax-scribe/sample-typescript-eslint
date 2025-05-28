[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `typeDeclaredInPackageDeclarationFile.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/typeOrValueSpecifiers/typeDeclaredInPackageDeclarationFile.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `matcher` | `RegExp` | const | `new RegExp(`${packageName}|${typesPackageName}`)` | ✗ |


---

## Functions

### `findParentModuleDeclaration(node: ts.Node): ts.ModuleDeclaration | undefined`

<details><summary>Code</summary>

```ts
function findParentModuleDeclaration(
  node: ts.Node,
): ts.ModuleDeclaration | undefined {
  switch (node.kind) {
    case ts.SyntaxKind.ModuleDeclaration:
      return ts.isStringLiteral((node as ts.ModuleDeclaration).name)
        ? (node as ts.ModuleDeclaration)
        : undefined;
    case ts.SyntaxKind.SourceFile:
      return undefined;
    default:
      return findParentModuleDeclaration(node.parent);
  }
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `ts.ModuleDeclaration | undefined`
- **Calls**:
  - `ts.isStringLiteral`
  - `findParentModuleDeclaration`
### `typeDeclaredInDeclareModule(packageName: string, declarations: ts.Node[]): boolean`

<details><summary>Code</summary>

```ts
function typeDeclaredInDeclareModule(
  packageName: string,
  declarations: ts.Node[],
): boolean {
  return declarations.some(
    declaration =>
      findParentModuleDeclaration(declaration)?.name.text === packageName,
  );
}
```
</details>

- **Parameters**:
  - `packageName: string`
  - `declarations: ts.Node[]`
- **Return Type**: `boolean`
- **Calls**:
  - `declarations.some`
  - `findParentModuleDeclaration`
### `typeDeclaredInDeclarationFile(packageName: string, declarationFiles: ts.SourceFile[], program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
function typeDeclaredInDeclarationFile(
  packageName: string,
  declarationFiles: ts.SourceFile[],
  program: ts.Program,
): boolean {
  // Handle scoped packages: if the name starts with @, remove it and replace / with __
  const typesPackageName = packageName.replace(/^@([^/]+)\//, '$1__');

  const matcher = new RegExp(`${packageName}|${typesPackageName}`);
  return declarationFiles.some(declaration => {
    const packageIdName = program.sourceFileToPackageName.get(declaration.path);
    return (
      packageIdName != null &&
      matcher.test(packageIdName) &&
      program.isSourceFileFromExternalLibrary(declaration)
    );
  });
}
```
</details>

- **Parameters**:
  - `packageName: string`
  - `declarationFiles: ts.SourceFile[]`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `packageName.replace`
  - `declarationFiles.some`
  - `program.sourceFileToPackageName.get`
  - `matcher.test`
  - `program.isSourceFileFromExternalLibrary`
- **Internal Comments**:
```
// Handle scoped packages: if the name starts with @, remove it and replace / with __ (x2)
```

### `typeDeclaredInPackageDeclarationFile(packageName: string, declarations: ts.Node[], declarationFiles: ts.SourceFile[], program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
export function typeDeclaredInPackageDeclarationFile(
  packageName: string,
  declarations: ts.Node[],
  declarationFiles: ts.SourceFile[],
  program: ts.Program,
): boolean {
  return (
    typeDeclaredInDeclareModule(packageName, declarations) ||
    typeDeclaredInDeclarationFile(packageName, declarationFiles, program)
  );
}
```
</details>

- **Parameters**:
  - `packageName: string`
  - `declarations: ts.Node[]`
  - `declarationFiles: ts.SourceFile[]`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `typeDeclaredInDeclareModule`
  - `typeDeclaredInDeclarationFile`

---