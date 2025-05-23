[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `TypeOrValueSpecifier.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 3
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/type-utils/src/TypeOrValueSpecifier.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `specifierNameMatches` | `./typeOrValueSpecifiers/specifierNameMatches` |
| `typeDeclaredInFile` | `./typeOrValueSpecifiers/typeDeclaredInFile` |
| `typeDeclaredInLib` | `./typeOrValueSpecifiers/typeDeclaredInLib` |
| `typeDeclaredInPackageDeclarationFile` | `./typeOrValueSpecifiers/typeDeclaredInPackageDeclarationFile` |


---

## Functions

### `typeMatchesSpecifier(type: ts.Type, specifier: TypeOrValueSpecifier, program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
export function typeMatchesSpecifier(
  type: ts.Type,
  specifier: TypeOrValueSpecifier,
  program: ts.Program,
): boolean {
  const wholeTypeMatches = ((): boolean => {
    if (tsutils.isIntrinsicErrorType(type)) {
      return false;
    }
    if (typeof specifier === 'string') {
      return specifierNameMatches(type, specifier);
    }
    if (!specifierNameMatches(type, specifier.name)) {
      return false;
    }
    const symbol = type.getSymbol() ?? type.aliasSymbol;
    const declarations = symbol?.getDeclarations() ?? [];
    const declarationFiles = declarations.map(declaration =>
      declaration.getSourceFile(),
    );
    switch (specifier.from) {
      case 'file':
        return typeDeclaredInFile(specifier.path, declarationFiles, program);
      case 'lib':
        return typeDeclaredInLib(declarationFiles, program);
      case 'package':
        return typeDeclaredInPackageDeclarationFile(
          specifier.package,
          declarations,
          declarationFiles,
          program,
        );
    }
  })();

  if (wholeTypeMatches) {
    return true;
  }

  if (
    tsutils.isIntersectionType(type) &&
    tsutils
      .intersectionConstituents(type)
      .some(part => typeMatchesSpecifier(part, specifier, program))
  ) {
    return true;
  }

  return false;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `specifier: TypeOrValueSpecifier`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `complex_call_4115`
  - `tsutils.isIntrinsicErrorType`
  - `specifierNameMatches (from ./typeOrValueSpecifiers/specifierNameMatches)`
  - `type.getSymbol`
  - `symbol?.getDeclarations`
  - `declarations.map`
  - `declaration.getSourceFile`
  - `typeDeclaredInFile (from ./typeOrValueSpecifiers/typeDeclaredInFile)`
  - `typeDeclaredInLib (from ./typeOrValueSpecifiers/typeDeclaredInLib)`
  - `typeDeclaredInPackageDeclarationFile (from ./typeOrValueSpecifiers/typeDeclaredInPackageDeclarationFile)`
  - `tsutils.isIntersectionType`
  - `tsutils
      .intersectionConstituents(type)
      .some`
  - `typeMatchesSpecifier`
### `typeMatchesSomeSpecifier(type: ts.Type, specifiers: TypeOrValueSpecifier[], program: ts.Program): boolean`

<details><summary>Code</summary>

```ts
(
  type: ts.Type,
  specifiers: TypeOrValueSpecifier[] = [],
  program: ts.Program,
): boolean =>
  specifiers.some(specifier => typeMatchesSpecifier(type, specifier, program))
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `specifiers: TypeOrValueSpecifier[]`
  - `program: ts.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `specifiers.some`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `FileSpecifier`

<details><summary>Interface Code</summary>

```ts
export interface FileSpecifier {
  from: 'file';

  /**
   * Type or value name(s) to match on.
   */
  name: string | string[];

  /**
   * A specific file the types or values must be declared in.
   */
  path?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `from` | `'file'` | ✗ |  |
| `name` | `string | string[]` | ✗ |  |
| `path` | `string` | ✓ |  |

### `LibSpecifier`

<details><summary>Interface Code</summary>

```ts
export interface LibSpecifier {
  from: 'lib';

  /**
   * Type or value name(s) to match on.
   */
  name: string | string[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `from` | `'lib'` | ✗ |  |
| `name` | `string | string[]` | ✗ |  |

### `PackageSpecifier`

<details><summary>Interface Code</summary>

```ts
export interface PackageSpecifier {
  from: 'package';

  /**
   * Type or value name(s) to match on.
   */
  name: string | string[];

  /**
   * Package name the type or value must be declared in.
   */
  package: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `from` | `'package'` | ✗ |  |
| `name` | `string | string[]` | ✗ |  |
| `package` | `string` | ✗ |  |


---

## Type Aliases

### `TypeOrValueSpecifier`

/**
 * A centralized format for rule options to describe specific _types_ and/or _values_.
 * See [TypeOrValueSpecifier](/packages/type-utils/type-or-value-specifier).
 */

```ts
type TypeOrValueSpecifier = | string
  | FileSpecifier
  | LibSpecifier
  | PackageSpecifier;
```


---