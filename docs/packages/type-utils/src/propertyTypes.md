[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `propertyTypes.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/propertyTypes.ts`**

## Functions

### `getTypeOfPropertyOfName(checker: ts.TypeChecker, type: ts.Type, name: string, escapedName: ts.__String): ts.Type | undefined`

<details><summary>Code</summary>

```ts
export function getTypeOfPropertyOfName(
  checker: ts.TypeChecker,
  type: ts.Type,
  name: string,
  escapedName?: ts.__String,
): ts.Type | undefined {
  // Most names are directly usable in the checker and aren't different from escaped names
  if (!escapedName || !isSymbol(escapedName)) {
    return checker.getTypeOfPropertyOfType(type, name);
  }

  // Symbolic names may differ in their escaped name compared to their human-readable name
  // https://github.com/typescript-eslint/typescript-eslint/issues/2143
  const escapedProperty = type
    .getProperties()
    .find(property => property.escapedName === escapedName);

  return escapedProperty
    ? checker.getDeclaredTypeOfSymbol(escapedProperty)
    : undefined;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
  - `name: string`
  - `escapedName: ts.__String`
- **Return Type**: `ts.Type | undefined`
- **Calls**:
  - `isSymbol`
  - `checker.getTypeOfPropertyOfType`
  - `type
    .getProperties()
    .find`
  - `checker.getDeclaredTypeOfSymbol`
- **Internal Comments**:
```
// Most names are directly usable in the checker and aren't different from escaped names
// Symbolic names may differ in their escaped name compared to their human-readable name (x2)
// https://github.com/typescript-eslint/typescript-eslint/issues/2143 (x2)
```

### `getTypeOfPropertyOfType(checker: ts.TypeChecker, type: ts.Type, property: ts.Symbol): ts.Type | undefined`

<details><summary>Code</summary>

```ts
export function getTypeOfPropertyOfType(
  checker: ts.TypeChecker,
  type: ts.Type,
  property: ts.Symbol,
): ts.Type | undefined {
  return getTypeOfPropertyOfName(
    checker,
    type,
    property.getName(),
    property.getEscapedName(),
  );
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
  - `property: ts.Symbol`
- **Return Type**: `ts.Type | undefined`
- **Calls**:
  - `getTypeOfPropertyOfName`
  - `property.getName`
  - `property.getEscapedName`
### `isSymbol(escapedName: string): boolean`

<details><summary>Code</summary>

```ts
function isSymbol(escapedName: string): boolean {
  return isKnownSymbol(escapedName) || isPrivateIdentifierSymbol(escapedName);
}
```
</details>

- **Parameters**:
  - `escapedName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `isKnownSymbol`
  - `isPrivateIdentifierSymbol`
### `isKnownSymbol(escapedName: string): boolean`

<details><summary>Code</summary>

```ts
function isKnownSymbol(escapedName: string): boolean {
  return escapedName.startsWith('__@');
}
```
</details>

- **Parameters**:
  - `escapedName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `escapedName.startsWith`
### `isPrivateIdentifierSymbol(escapedName: string): boolean`

<details><summary>Code</summary>

```ts
function isPrivateIdentifierSymbol(escapedName: string): boolean {
  return escapedName.startsWith('__#');
}
```
</details>

- **Parameters**:
  - `escapedName: string`
- **Return Type**: `boolean`
- **Calls**:
  - `escapedName.startsWith`

---