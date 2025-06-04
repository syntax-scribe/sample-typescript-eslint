[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `predicates.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 11 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/predicates.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `debug` | `debug` |
| `isTypeFlagSet` | `./typeFlagUtils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `Nullable` | `number` | const | `ts.TypeFlags.Undefined | ts.TypeFlags.Null` | ✗ |
| `ObjectFlagsType` | `number` | const | `ts.TypeFlags.Any |
  Nullable |
  ts.TypeFlags.Never |
  ts.TypeFlags.Object |
  ts.TypeFlags.Union |
  ts.TypeFlags.Intersection` | ✗ |
| `objectTypeFlags` | `any` | const | `(type as ts.ObjectType).objectFlags` | ✗ |
| `typeAndBaseTypes` | `ts.Type[]` | const | `[type]` | ✗ |


---

## Functions

### `isNullableType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isNullableType(type: ts.Type): boolean {
  return isTypeFlagSet(
    type,
    ts.TypeFlags.Any |
      ts.TypeFlags.Unknown |
      ts.TypeFlags.Null |
      ts.TypeFlags.Undefined |
      ts.TypeFlags.Void,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the given type is (or accepts) nullable
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
### `isTypeArrayTypeOrUnionOfArrayTypes(type: ts.Type, checker: ts.TypeChecker): boolean`

<details><summary>Code</summary>

```ts
export function isTypeArrayTypeOrUnionOfArrayTypes(
  type: ts.Type,
  checker: ts.TypeChecker,
): boolean {
  for (const t of tsutils.unionConstituents(type)) {
    if (!checker.isArrayType(t)) {
      return false;
    }
  }

  return true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks if the given type is either an array type,
 * or a union made up solely of array types.
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.unionConstituents`
  - `checker.isArrayType`
### `isTypeNeverType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isTypeNeverType(type: ts.Type): boolean {
  return isTypeFlagSet(type, ts.TypeFlags.Never);
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns true if the type is `never`
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
### `isTypeUnknownType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isTypeUnknownType(type: ts.Type): boolean {
  return isTypeFlagSet(type, ts.TypeFlags.Unknown);
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns true if the type is `unknown`
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
### `isTypeReferenceType(type: ts.Type): type is ts.TypeReference`

<details><summary>Code</summary>

```ts
export function isTypeReferenceType(type: ts.Type): type is ts.TypeReference {
  if ((type.flags & ObjectFlagsType) === 0) {
    return false;
  }
  const objectTypeFlags = (type as ts.ObjectType).objectFlags;
  return (objectTypeFlags & ts.ObjectFlags.Reference) !== 0;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `type is ts.TypeReference`
### `isTypeAnyType(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function isTypeAnyType(type: ts.Type): boolean {
  if (isTypeFlagSet(type, ts.TypeFlags.Any)) {
    if (type.intrinsicName === 'error') {
      log('Found an "error" any type');
    }
    return true;
  }
  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns true if the type is `any`
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
  - `log`
### `isTypeAnyArrayType(type: ts.Type, checker: ts.TypeChecker): boolean`

<details><summary>Code</summary>

```ts
export function isTypeAnyArrayType(
  type: ts.Type,
  checker: ts.TypeChecker,
): boolean {
  return (
    checker.isArrayType(type) &&
    isTypeAnyType(checker.getTypeArguments(type)[0])
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns true if the type is `any[]`
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.isArrayType`
  - `isTypeAnyType`
  - `checker.getTypeArguments`
### `isTypeUnknownArrayType(type: ts.Type, checker: ts.TypeChecker): boolean`

<details><summary>Code</summary>

```ts
export function isTypeUnknownArrayType(
  type: ts.Type,
  checker: ts.TypeChecker,
): boolean {
  return (
    checker.isArrayType(type) &&
    isTypeUnknownType(checker.getTypeArguments(type)[0])
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns true if the type is `unknown[]`
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.isArrayType`
  - `isTypeUnknownType`
  - `checker.getTypeArguments`
### `typeIsOrHasBaseType(type: ts.Type, parentType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
export function typeIsOrHasBaseType(
  type: ts.Type,
  parentType: ts.Type,
): boolean {
  const parentSymbol = parentType.getSymbol();
  if (!type.getSymbol() || !parentSymbol) {
    return false;
  }

  const typeAndBaseTypes = [type];
  const ancestorTypes = type.getBaseTypes();

  if (ancestorTypes) {
    typeAndBaseTypes.push(...ancestorTypes);
  }

  for (const baseType of typeAndBaseTypes) {
    const baseSymbol = baseType.getSymbol();
    if (baseSymbol && baseSymbol.name === parentSymbol.name) {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether a type is an instance of the parent type, including for the parent's base types.
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `parentType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `parentType.getSymbol`
  - `type.getSymbol`
  - `type.getBaseTypes`
  - `typeAndBaseTypes.push`
  - `baseType.getSymbol`
### `isTypeBigIntLiteralType(type: ts.Type): type is ts.BigIntLiteralType`

<details><summary>Code</summary>

```ts
export function isTypeBigIntLiteralType(
  type: ts.Type,
): type is ts.BigIntLiteralType {
  return isTypeFlagSet(type, ts.TypeFlags.BigIntLiteral);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `type is ts.BigIntLiteralType`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`
### `isTypeTemplateLiteralType(type: ts.Type): type is ts.TemplateLiteralType`

<details><summary>Code</summary>

```ts
export function isTypeTemplateLiteralType(
  type: ts.Type,
): type is ts.TemplateLiteralType {
  return isTypeFlagSet(type, ts.TypeFlags.TemplateLiteral);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `type is ts.TemplateLiteralType`
- **Calls**:
  - `isTypeFlagSet (from ./typeFlagUtils)`

---