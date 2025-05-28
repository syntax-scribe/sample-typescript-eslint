[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `TypeOrValueSpecifier.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `typeOrValueSpecifiersSchema` | `JSONSchema4` | const | `{
  items: {
    oneOf: [
      {
        type: 'string',
      },
      {
        additionalProperties: false,
        properties: {
          from: {
            enum: ['file'],
            type: 'string',
          },
          name: {
            oneOf: [
              {
                type: 'string',
              },
              {
                items: {
                  type: 'string',
                },
                minItems: 1,
                type: 'array',
                uniqueItems: true,
              },
            ],
          },
          path: {
            type: 'string',
          },
        },
        required: ['from', 'name'],
        type: 'object',
      },
      {
        additionalProperties: false,
        properties: {
          from: {
            enum: ['lib'],
            type: 'string',
          },
          name: {
            oneOf: [
              {
                type: 'string',
              },
              {
                items: {
                  type: 'string',
                },
                minItems: 1,
                type: 'array',
                uniqueItems: true,
              },
            ],
          },
        },
        required: ['from', 'name'],
        type: 'object',
      },
      {
        additionalProperties: false,
        properties: {
          from: {
            enum: ['package'],
            type: 'string',
          },
          name: {
            oneOf: [
              {
                type: 'string',
              },
              {
                items: {
                  type: 'string',
                },
                minItems: 1,
                type: 'array',
                uniqueItems: true,
              },
            ],
          },
          package: {
            type: 'string',
          },
        },
        required: ['from', 'name', 'package'],
        type: 'object',
      },
    ],
  },
  type: 'array',
} as const satisfies JSONSchema4` | ✓ |
| `symbol` | `any` | const | `type.getSymbol() ?? type.aliasSymbol` | ✗ |
| `declarations` | `any` | const | `symbol?.getDeclarations() ?? []` | ✗ |


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