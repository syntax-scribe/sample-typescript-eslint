[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isTypeReadonly.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 7
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/isTypeReadonly.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `TypeOrValueSpecifier` | `./TypeOrValueSpecifier` |
| `getTypeOfPropertyOfType` | `./propertyTypes` |
| `typeMatchesSomeSpecifier` | `./TypeOrValueSpecifier` |
| `typeOrValueSpecifiersSchema` | `./TypeOrValueSpecifier` |


---

## Functions

### `hasSymbol(node: ts.Node): node is { symbol: ts.Symbol } & ts.Node`

<details><summary>Code</summary>

```ts
function hasSymbol(node: ts.Node): node is { symbol: ts.Symbol } & ts.Node {
  return Object.hasOwn(node, 'symbol');
}
```
</details>

- **Parameters**:
  - `node: ts.Node`
- **Return Type**: `node is { symbol: ts.Symbol } & ts.Node`
- **Calls**:
  - `Object.hasOwn`
### `isTypeReadonlyArrayOrTuple(program: ts.Program, type: ts.Type, options: ReadonlynessOptions, seenTypes: Set<ts.Type>): Readonlyness`

<details><summary>Code</summary>

```ts
function isTypeReadonlyArrayOrTuple(
  program: ts.Program,
  type: ts.Type,
  options: ReadonlynessOptions,
  seenTypes: Set<ts.Type>,
): Readonlyness {
  const checker = program.getTypeChecker();
  function checkTypeArguments(arrayType: ts.TypeReference): Readonlyness {
    const typeArguments = checker.getTypeArguments(arrayType);

    // this shouldn't happen in reality as:
    // - tuples require at least 1 type argument
    // - ReadonlyArray requires at least 1 type argument
    /* istanbul ignore if */ if (typeArguments.length === 0) {
      return Readonlyness.Readonly;
    }

    // validate the element types are also readonly
    if (
      typeArguments.some(
        typeArg =>
          isTypeReadonlyRecurser(program, typeArg, options, seenTypes) ===
          Readonlyness.Mutable,
      )
    ) {
      return Readonlyness.Mutable;
    }
    return Readonlyness.Readonly;
  }

  if (checker.isArrayType(type)) {
    const symbol = ESLintUtils.nullThrows(
      type.getSymbol(),
      ESLintUtils.NullThrowsReasons.MissingToken('symbol', 'array type'),
    );
    const escapedName = symbol.getEscapedName();
    // eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
    if (escapedName === 'Array') {
      return Readonlyness.Mutable;
    }

    return checkTypeArguments(type);
  }

  if (checker.isTupleType(type)) {
    if (!type.target.readonly) {
      return Readonlyness.Mutable;
    }

    return checkTypeArguments(type);
  }

  return Readonlyness.UnknownType;
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `options: ReadonlynessOptions`
  - `seenTypes: Set<ts.Type>`
- **Return Type**: `Readonlyness`
- **Calls**:
  - `program.getTypeChecker`
  - `checker.getTypeArguments`
  - `typeArguments.some`
  - `isTypeReadonlyRecurser`
  - `checker.isArrayType`
  - `ESLintUtils.nullThrows`
  - `type.getSymbol`
  - `ESLintUtils.NullThrowsReasons.MissingToken`
  - `symbol.getEscapedName`
  - `checkTypeArguments`
  - `checker.isTupleType`
- **Internal Comments**:
```
// this shouldn't happen in reality as:
// - tuples require at least 1 type argument
// - ReadonlyArray requires at least 1 type argument
/* istanbul ignore if */
// validate the element types are also readonly
// eslint-disable-next-line @typescript-eslint/no-unsafe-enum-comparison
```

### `checkTypeArguments(arrayType: ts.TypeReference): Readonlyness`

<details><summary>Code</summary>

```ts
function checkTypeArguments(arrayType: ts.TypeReference): Readonlyness {
    const typeArguments = checker.getTypeArguments(arrayType);

    // this shouldn't happen in reality as:
    // - tuples require at least 1 type argument
    // - ReadonlyArray requires at least 1 type argument
    /* istanbul ignore if */ if (typeArguments.length === 0) {
      return Readonlyness.Readonly;
    }

    // validate the element types are also readonly
    if (
      typeArguments.some(
        typeArg =>
          isTypeReadonlyRecurser(program, typeArg, options, seenTypes) ===
          Readonlyness.Mutable,
      )
    ) {
      return Readonlyness.Mutable;
    }
    return Readonlyness.Readonly;
  }
```
</details>

- **Parameters**:
  - `arrayType: ts.TypeReference`
- **Return Type**: `Readonlyness`
- **Calls**:
  - `checker.getTypeArguments`
  - `typeArguments.some`
  - `isTypeReadonlyRecurser`
- **Internal Comments**:
```
// this shouldn't happen in reality as:
// - tuples require at least 1 type argument
// - ReadonlyArray requires at least 1 type argument
/* istanbul ignore if */
// validate the element types are also readonly
```

### `isTypeReadonlyObject(program: ts.Program, type: ts.Type, options: ReadonlynessOptions, seenTypes: Set<ts.Type>): Readonlyness`

<details><summary>Code</summary>

```ts
function isTypeReadonlyObject(
  program: ts.Program,
  type: ts.Type,
  options: ReadonlynessOptions,
  seenTypes: Set<ts.Type>,
): Readonlyness {
  const checker = program.getTypeChecker();
  function checkIndexSignature(kind: ts.IndexKind): Readonlyness {
    const indexInfo = checker.getIndexInfoOfType(type, kind);
    if (indexInfo) {
      if (!indexInfo.isReadonly) {
        return Readonlyness.Mutable;
      }

      if (indexInfo.type === type || seenTypes.has(indexInfo.type)) {
        return Readonlyness.Readonly;
      }

      return isTypeReadonlyRecurser(
        program,
        indexInfo.type,
        options,
        seenTypes,
      );
    }

    return Readonlyness.UnknownType;
  }

  const properties = type.getProperties();
  if (properties.length) {
    // ensure the properties are marked as readonly
    for (const property of properties) {
      if (options.treatMethodsAsReadonly) {
        if (
          property.valueDeclaration != null &&
          hasSymbol(property.valueDeclaration) &&
          tsutils.isSymbolFlagSet(
            property.valueDeclaration.symbol,
            ts.SymbolFlags.Method,
          )
        ) {
          continue;
        }

        const declarations = property.getDeclarations();
        const lastDeclaration =
          declarations != null && declarations.length > 0
            ? declarations[declarations.length - 1]
            : undefined;
        if (
          lastDeclaration != null &&
          hasSymbol(lastDeclaration) &&
          tsutils.isSymbolFlagSet(lastDeclaration.symbol, ts.SymbolFlags.Method)
        ) {
          continue;
        }
      }

      if (
        tsutils.isPropertyReadonlyInType(
          type,
          property.getEscapedName(),
          checker,
        )
      ) {
        continue;
      }

      const name = ts.getNameOfDeclaration(property.valueDeclaration);
      if (name && ts.isPrivateIdentifier(name)) {
        continue;
      }

      return Readonlyness.Mutable;
    }

    // all properties were readonly
    // now ensure that all of the values are readonly also.

    // do this after checking property readonly-ness as a perf optimization,
    // as we might be able to bail out early due to a mutable property before
    // doing this deep, potentially expensive check.
    for (const property of properties) {
      const propertyType = ESLintUtils.nullThrows(
        getTypeOfPropertyOfType(checker, type, property),
        ESLintUtils.NullThrowsReasons.MissingToken(
          `property "${property.name}"`,
          'type',
        ),
      );

      // handle recursive types.
      // we only need this simple check, because a mutable recursive type will break via the above prop readonly check
      if (seenTypes.has(propertyType)) {
        continue;
      }

      if (
        isTypeReadonlyRecurser(program, propertyType, options, seenTypes) ===
        Readonlyness.Mutable
      ) {
        return Readonlyness.Mutable;
      }
    }
  }

  const isStringIndexSigReadonly = checkIndexSignature(ts.IndexKind.String);
  if (isStringIndexSigReadonly === Readonlyness.Mutable) {
    return isStringIndexSigReadonly;
  }

  const isNumberIndexSigReadonly = checkIndexSignature(ts.IndexKind.Number);
  if (isNumberIndexSigReadonly === Readonlyness.Mutable) {
    return isNumberIndexSigReadonly;
  }

  return Readonlyness.Readonly;
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `options: ReadonlynessOptions`
  - `seenTypes: Set<ts.Type>`
- **Return Type**: `Readonlyness`
- **Calls**:
  - `program.getTypeChecker`
  - `checker.getIndexInfoOfType`
  - `seenTypes.has`
  - `isTypeReadonlyRecurser`
  - `type.getProperties`
  - `hasSymbol`
  - `tsutils.isSymbolFlagSet`
  - `property.getDeclarations`
  - `tsutils.isPropertyReadonlyInType`
  - `property.getEscapedName`
  - `ts.getNameOfDeclaration`
  - `ts.isPrivateIdentifier`
  - `ESLintUtils.nullThrows`
  - `getTypeOfPropertyOfType (from ./propertyTypes)`
  - `ESLintUtils.NullThrowsReasons.MissingToken`
  - `checkIndexSignature`
- **Internal Comments**:
```
// ensure the properties are marked as readonly
// all properties were readonly
// now ensure that all of the values are readonly also.
// do this after checking property readonly-ness as a perf optimization,
// as we might be able to bail out early due to a mutable property before
// doing this deep, potentially expensive check.
// handle recursive types.
// we only need this simple check, because a mutable recursive type will break via the above prop readonly check
```

### `checkIndexSignature(kind: ts.IndexKind): Readonlyness`

<details><summary>Code</summary>

```ts
function checkIndexSignature(kind: ts.IndexKind): Readonlyness {
    const indexInfo = checker.getIndexInfoOfType(type, kind);
    if (indexInfo) {
      if (!indexInfo.isReadonly) {
        return Readonlyness.Mutable;
      }

      if (indexInfo.type === type || seenTypes.has(indexInfo.type)) {
        return Readonlyness.Readonly;
      }

      return isTypeReadonlyRecurser(
        program,
        indexInfo.type,
        options,
        seenTypes,
      );
    }

    return Readonlyness.UnknownType;
  }
```
</details>

- **Parameters**:
  - `kind: ts.IndexKind`
- **Return Type**: `Readonlyness`
- **Calls**:
  - `checker.getIndexInfoOfType`
  - `seenTypes.has`
  - `isTypeReadonlyRecurser`
### `isTypeReadonlyRecurser(program: ts.Program, type: ts.Type, options: ReadonlynessOptions, seenTypes: Set<ts.Type>): Readonlyness.Mutable | Readonlyness.Readonly`

<details><summary>Code</summary>

```ts
function isTypeReadonlyRecurser(
  program: ts.Program,
  type: ts.Type,
  options: ReadonlynessOptions,
  seenTypes: Set<ts.Type>,
): Readonlyness.Mutable | Readonlyness.Readonly {
  const checker = program.getTypeChecker();
  seenTypes.add(type);

  if (typeMatchesSomeSpecifier(type, options.allow, program)) {
    return Readonlyness.Readonly;
  }

  if (tsutils.isUnionType(type)) {
    // all types in the union must be readonly
    const result = tsutils
      .unionConstituents(type)
      .every(
        t =>
          seenTypes.has(t) ||
          isTypeReadonlyRecurser(program, t, options, seenTypes) ===
            Readonlyness.Readonly,
      );
    const readonlyness = result ? Readonlyness.Readonly : Readonlyness.Mutable;
    return readonlyness;
  }

  if (tsutils.isIntersectionType(type)) {
    // Special case for handling arrays/tuples (as readonly arrays/tuples always have mutable methods).
    if (
      type.types.some(t => checker.isArrayType(t) || checker.isTupleType(t))
    ) {
      const allReadonlyParts = type.types.every(
        t =>
          seenTypes.has(t) ||
          isTypeReadonlyRecurser(program, t, options, seenTypes) ===
            Readonlyness.Readonly,
      );
      return allReadonlyParts ? Readonlyness.Readonly : Readonlyness.Mutable;
    }

    // Normal case.
    const isReadonlyObject = isTypeReadonlyObject(
      program,
      type,
      options,
      seenTypes,
    );
    if (isReadonlyObject !== Readonlyness.UnknownType) {
      return isReadonlyObject;
    }
  }

  if (tsutils.isConditionalType(type)) {
    const result = [type.root.node.trueType, type.root.node.falseType]
      .map(checker.getTypeFromTypeNode)
      .every(
        t =>
          seenTypes.has(t) ||
          isTypeReadonlyRecurser(program, t, options, seenTypes) ===
            Readonlyness.Readonly,
      );

    const readonlyness = result ? Readonlyness.Readonly : Readonlyness.Mutable;
    return readonlyness;
  }

  // all non-object, non-intersection types are readonly.
  // this should only be primitive types
  if (!tsutils.isObjectType(type)) {
    return Readonlyness.Readonly;
  }

  // pure function types are readonly
  if (
    type.getCallSignatures().length > 0 &&
    type.getProperties().length === 0
  ) {
    return Readonlyness.Readonly;
  }

  const isReadonlyArray = isTypeReadonlyArrayOrTuple(
    program,
    type,
    options,
    seenTypes,
  );
  if (isReadonlyArray !== Readonlyness.UnknownType) {
    return isReadonlyArray;
  }

  const isReadonlyObject = isTypeReadonlyObject(
    program,
    type,
    options,
    seenTypes,
  );
  /* istanbul ignore else */ if (
    isReadonlyObject !== Readonlyness.UnknownType
  ) {
    return isReadonlyObject;
  }

  throw new Error('Unhandled type');
}
```
</details>

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `options: ReadonlynessOptions`
  - `seenTypes: Set<ts.Type>`
- **Return Type**: `Readonlyness.Mutable | Readonlyness.Readonly`
- **Calls**:
  - `program.getTypeChecker`
  - `seenTypes.add`
  - `typeMatchesSomeSpecifier (from ./TypeOrValueSpecifier)`
  - `tsutils.isUnionType`
  - `tsutils
      .unionConstituents(type)
      .every`
  - `seenTypes.has`
  - `isTypeReadonlyRecurser`
  - `tsutils.isIntersectionType`
  - `type.types.some`
  - `checker.isArrayType`
  - `checker.isTupleType`
  - `type.types.every`
  - `isTypeReadonlyObject`
  - `tsutils.isConditionalType`
  - `[type.root.node.trueType, type.root.node.falseType]
      .map(checker.getTypeFromTypeNode)
      .every`
  - `tsutils.isObjectType`
  - `type.getCallSignatures`
  - `type.getProperties`
  - `isTypeReadonlyArrayOrTuple`
- **Internal Comments**:
```
// all types in the union must be readonly (x2)
// Special case for handling arrays/tuples (as readonly arrays/tuples always have mutable methods).
// Normal case. (x2)
// all non-object, non-intersection types are readonly.
// this should only be primitive types
// pure function types are readonly
/* istanbul ignore else */
```

### `isTypeReadonly(program: ts.Program, type: ts.Type, options: ReadonlynessOptions): boolean`

<details><summary>Code</summary>

```ts
export function isTypeReadonly(
  program: ts.Program,
  type: ts.Type,
  options: ReadonlynessOptions = readonlynessOptionsDefaults,
): boolean {
  return (
    isTypeReadonlyRecurser(program, type, options, new Set()) ===
    Readonlyness.Readonly
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the given type is readonly
 */
```

- **Parameters**:
  - `program: ts.Program`
  - `type: ts.Type`
  - `options: ReadonlynessOptions`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeReadonlyRecurser`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `ReadonlynessOptions`

<details><summary>Interface Code</summary>

```ts
export interface ReadonlynessOptions {
  readonly allow?: TypeOrValueSpecifier[];
  readonly treatMethodsAsReadonly?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allow` | `TypeOrValueSpecifier[]` | ✓ |  |
| `treatMethodsAsReadonly` | `boolean` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---