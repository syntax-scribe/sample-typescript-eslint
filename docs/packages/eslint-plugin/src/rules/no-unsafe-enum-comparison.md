[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unsafe-enum-comparison.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 5 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unsafe-enum-comparison.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `getStaticValue` | `../util` |
| `getEnumKeyForLiteral` | `./enum-utils/shared` |
| `getEnumLiterals` | `./enum-utils/shared` |
| `getEnumTypes` | `./enum-utils/shared` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `leftEnumValueTypes` | `Set<any>` | const | `new Set(leftTypeParts.map(getEnumValueType))` | ✗ |
| `rightEnumTypes` | `Set<ts.Type>` | const | `new Set(getEnumTypes(typeChecker, rightType))` | ✗ |


---

## Functions

### `typeViolates(leftTypeParts: ts.Type[], rightType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function typeViolates(leftTypeParts: ts.Type[], rightType: ts.Type): boolean {
  const leftEnumValueTypes = new Set(leftTypeParts.map(getEnumValueType));

  return (
    (leftEnumValueTypes.has(ts.TypeFlags.Number) && isNumberLike(rightType)) ||
    (leftEnumValueTypes.has(ts.TypeFlags.String) && isStringLike(rightType))
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns Whether the right type is an unsafe comparison against any left type.
 */
```

- **Parameters**:
  - `leftTypeParts: ts.Type[]`
  - `rightType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `leftTypeParts.map`
  - `leftEnumValueTypes.has`
  - `isNumberLike`
  - `isStringLike`
### `isNumberLike(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isNumberLike(type: ts.Type): boolean {
  const typeParts = tsutils.intersectionConstituents(type);

  return typeParts.some(typePart => {
    return tsutils.isTypeFlagSet(
      typePart,
      ts.TypeFlags.Number | ts.TypeFlags.NumberLike,
    );
  });
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.intersectionConstituents`
  - `typeParts.some`
  - `tsutils.isTypeFlagSet`
### `isStringLike(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isStringLike(type: ts.Type): boolean {
  const typeParts = tsutils.intersectionConstituents(type);

  return typeParts.some(typePart => {
    return tsutils.isTypeFlagSet(
      typePart,
      ts.TypeFlags.String | ts.TypeFlags.StringLike,
    );
  });
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils.intersectionConstituents`
  - `typeParts.some`
  - `tsutils.isTypeFlagSet`
### `getEnumValueType(type: ts.Type): ts.TypeFlags | undefined`

<details><summary>Code</summary>

```ts
function getEnumValueType(type: ts.Type): ts.TypeFlags | undefined {
  return tsutils.isTypeFlagSet(type, ts.TypeFlags.EnumLike)
    ? tsutils.isTypeFlagSet(type, ts.TypeFlags.NumberLiteral)
      ? ts.TypeFlags.Number
      : ts.TypeFlags.String
    : undefined;
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns What type a type's enum value is (number or string), if either.
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `ts.TypeFlags | undefined`
- **Calls**:
  - `tsutils.isTypeFlagSet`
### `isMismatchedComparison(leftType: ts.Type, rightType: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isMismatchedComparison(
      leftType: ts.Type,
      rightType: ts.Type,
    ): boolean {
      // Allow comparisons that don't have anything to do with enums:
      //
      // ```ts
      // 1 === 2;
      // ```
      const leftEnumTypes = getEnumTypes(typeChecker, leftType);
      const rightEnumTypes = new Set(getEnumTypes(typeChecker, rightType));
      if (leftEnumTypes.length === 0 && rightEnumTypes.size === 0) {
        return false;
      }

      // Allow comparisons that share an enum type:
      //
      // ```ts
      // Fruit.Apple === Fruit.Banana;
      // ```
      for (const leftEnumType of leftEnumTypes) {
        if (rightEnumTypes.has(leftEnumType)) {
          return false;
        }
      }

      // We need to split the type into the union type parts in order to find
      // valid enum comparisons like:
      //
      // ```ts
      // declare const something: Fruit | Vegetable;
      // something === Fruit.Apple;
      // ```
      const leftTypeParts = tsutils.unionConstituents(leftType);
      const rightTypeParts = tsutils.unionConstituents(rightType);

      // If a type exists in both sides, we consider this comparison safe:
      //
      // ```ts
      // declare const fruit: Fruit.Apple | 0;
      // fruit === 0;
      // ```
      for (const leftTypePart of leftTypeParts) {
        if (rightTypeParts.includes(leftTypePart)) {
          return false;
        }
      }

      return (
        typeViolates(leftTypeParts, rightType) ||
        typeViolates(rightTypeParts, leftType)
      );
    }
```
</details>

- **Parameters**:
  - `leftType: ts.Type`
  - `rightType: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `getEnumTypes (from ./enum-utils/shared)`
  - `rightEnumTypes.has`
  - `tsutils.unionConstituents`
  - `rightTypeParts.includes`
  - `typeViolates`
- **Internal Comments**:
```
// Allow comparisons that don't have anything to do with enums: (x2)
// (x6)
// ```ts (x6)
// 1 === 2; (x2)
// ``` (x6)
// Allow comparisons that share an enum type:
// Fruit.Apple === Fruit.Banana;
// We need to split the type into the union type parts in order to find (x2)
// valid enum comparisons like: (x2)
// declare const something: Fruit | Vegetable; (x2)
// something === Fruit.Apple; (x2)
// If a type exists in both sides, we consider this comparison safe:
// declare const fruit: Fruit.Apple | 0;
// fruit === 0;
```


---