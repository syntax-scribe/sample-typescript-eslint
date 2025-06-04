[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getTypeName.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/getTypeName.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `typeParamDecl` | `any` | const | `decls?.[0]` | ✗ |


---

## Functions

### `getTypeName(typeChecker: ts.TypeChecker, type: ts.Type): string`

<details><summary>Code</summary>

```ts
export function getTypeName(
  typeChecker: ts.TypeChecker,
  type: ts.Type,
): string {
  // It handles `string` and string literal types as string.
  if ((type.flags & ts.TypeFlags.StringLike) !== 0) {
    return 'string';
  }

  // If the type is a type parameter which extends primitive string types,
  // but it was not recognized as a string like. So check the constraint
  // type of the type parameter.
  if ((type.flags & ts.TypeFlags.TypeParameter) !== 0) {
    // `type.getConstraint()` method doesn't return the constraint type of
    // the type parameter for some reason. So this gets the constraint type
    // via AST.
    const symbol = type.getSymbol();
    const decls = symbol?.getDeclarations();
    const typeParamDecl = decls?.[0];
    if (
      typeParamDecl != null &&
      ts.isTypeParameterDeclaration(typeParamDecl) &&
      typeParamDecl.constraint != null
    ) {
      return getTypeName(
        typeChecker,
        typeChecker.getTypeFromTypeNode(typeParamDecl.constraint),
      );
    }
  }

  // If the type is a union and all types in the union are string like,
  // return `string`. For example:
  // - `"a" | "b"` is string.
  // - `string | string[]` is not string.
  if (
    type.isUnion() &&
    type.types
      .map(value => getTypeName(typeChecker, value))
      .every(t => t === 'string')
  ) {
    return 'string';
  }

  // If the type is an intersection and a type in the intersection is string
  // like, return `string`. For example: `string & {__htmlEscaped: void}`
  if (
    type.isIntersection() &&
    type.types
      .map(value => getTypeName(typeChecker, value))
      .some(t => t === 'string')
  ) {
    return 'string';
  }

  return typeChecker.typeToString(type);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Get the type name of a given type.
 * @param typeChecker The context sensitive TypeScript TypeChecker.
 * @param type The type to get the name of.
 */
```

- **Parameters**:
  - `typeChecker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `string`
- **Calls**:
  - `type.getSymbol`
  - `symbol?.getDeclarations`
  - `ts.isTypeParameterDeclaration`
  - `getTypeName`
  - `typeChecker.getTypeFromTypeNode`
  - `type.isUnion`
  - `type.types
      .map(value => getTypeName(typeChecker, value))
      .every`
  - `type.isIntersection`
  - `type.types
      .map(value => getTypeName(typeChecker, value))
      .some`
  - `typeChecker.typeToString`
- **Internal Comments**:
```
// It handles `string` and string literal types as string.
// If the type is a type parameter which extends primitive string types,
// but it was not recognized as a string like. So check the constraint
// type of the type parameter.
// `type.getConstraint()` method doesn't return the constraint type of (x2)
// the type parameter for some reason. So this gets the constraint type (x2)
// via AST. (x2)
// If the type is a union and all types in the union are string like,
// return `string`. For example:
// - `"a" | "b"` is string.
// - `string | string[]` is not string.
// If the type is an intersection and a type in the intersection is string
// like, return `string`. For example: `string & {__htmlEscaped: void}`
```


---