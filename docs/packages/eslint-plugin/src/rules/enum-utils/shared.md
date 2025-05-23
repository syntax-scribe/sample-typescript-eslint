[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `shared.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/enum-utils/shared.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isTypeFlagSet` | `../../util` |


---

## Functions

### `getBaseEnumType(typeChecker: ts.TypeChecker, type: ts.Type): ts.Type`

<details><summary>Code</summary>

```ts
function getBaseEnumType(typeChecker: ts.TypeChecker, type: ts.Type): ts.Type {
  // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
  const symbol = type.getSymbol()!;
  if (!tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.EnumMember)) {
    return type;
  }

  return typeChecker.getTypeAtLocation(
    (symbol.valueDeclaration as ts.EnumMember).parent,
  );
}
```
</details>

- **Parameters**:
  - `typeChecker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `ts.Type`
- **Calls**:
  - `type.getSymbol`
  - `tsutils.isSymbolFlagSet`
  - `typeChecker.getTypeAtLocation`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `getEnumLiterals(type: ts.Type): ts.LiteralType[]`

<details><summary>Code</summary>

```ts
export function getEnumLiterals(type: ts.Type): ts.LiteralType[] {
  return tsutils
    .unionConstituents(type)
    .filter((subType): subType is ts.LiteralType =>
      isTypeFlagSet(subType, ts.TypeFlags.EnumLiteral),
    );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Retrieve only the Enum literals from a type. for example:
 * - 123 --> []
 * - {} --> []
 * - Fruit.Apple --> [Fruit.Apple]
 * - Fruit.Apple | Vegetable.Lettuce --> [Fruit.Apple, Vegetable.Lettuce]
 * - Fruit.Apple | Vegetable.Lettuce | 123 --> [Fruit.Apple, Vegetable.Lettuce]
 * - T extends Fruit --> [Fruit]
 */
```

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `ts.LiteralType[]`
- **Calls**:
  - `tsutils
    .unionConstituents(type)
    .filter`
  - `isTypeFlagSet (from ../../util)`
### `getEnumTypes(typeChecker: ts.TypeChecker, type: ts.Type): ts.Type[]`

<details><summary>Code</summary>

```ts
export function getEnumTypes(
  typeChecker: ts.TypeChecker,
  type: ts.Type,
): ts.Type[] {
  return getEnumLiterals(type).map(type => getBaseEnumType(typeChecker, type));
}
```
</details>

- **JSDoc**:
```ts
/**
 * A type can have 0 or more enum types. For example:
 * - 123 --> []
 * - {} --> []
 * - Fruit.Apple --> [Fruit]
 * - Fruit.Apple | Vegetable.Lettuce --> [Fruit, Vegetable]
 * - Fruit.Apple | Vegetable.Lettuce | 123 --> [Fruit, Vegetable]
 * - T extends Fruit --> [Fruit]
 */
```

- **Parameters**:
  - `typeChecker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `ts.Type[]`
- **Calls**:
  - `getEnumLiterals(type).map`
  - `getBaseEnumType`
### `getEnumKeyForLiteral(enumLiterals: ts.LiteralType[], literal: unknown): string | null`

<details><summary>Code</summary>

```ts
export function getEnumKeyForLiteral(
  enumLiterals: ts.LiteralType[],
  literal: unknown,
): string | null {
  for (const enumLiteral of enumLiterals) {
    if (enumLiteral.value === literal) {
      const { symbol } = enumLiteral;

      const memberDeclaration = symbol.valueDeclaration as ts.EnumMember;
      const enumDeclaration = memberDeclaration.parent;

      const memberNameIdentifier = memberDeclaration.name;
      const enumName = enumDeclaration.name.text;

      switch (memberNameIdentifier.kind) {
        case ts.SyntaxKind.Identifier:
          return `${enumName}.${memberNameIdentifier.text}`;

        case ts.SyntaxKind.StringLiteral: {
          const memberName = memberNameIdentifier.text.replaceAll("'", "\\'");

          return `${enumName}['${memberName}']`;
        }

        case ts.SyntaxKind.ComputedPropertyName:
          return `${enumName}[${memberNameIdentifier.expression.getText()}]`;

        default:
          break;
      }
    }
  }

  return null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns the enum key that matches the given literal node, or null if none
 * match. For example:
 * ```ts
 * enum Fruit {
 *   Apple = 'apple',
 *   Banana = 'banana',
 * }
 *
 * getEnumKeyForLiteral([Fruit.Apple, Fruit.Banana], 'apple') --> 'Fruit.Apple'
 * getEnumKeyForLiteral([Fruit.Apple, Fruit.Banana], 'banana') --> 'Fruit.Banana'
 * getEnumKeyForLiteral([Fruit.Apple, Fruit.Banana], 'cherry') --> null
 * ```
 */
```

- **Parameters**:
  - `enumLiterals: ts.LiteralType[]`
  - `literal: unknown`
- **Return Type**: `string | null`
- **Calls**:
  - `memberNameIdentifier.text.replaceAll`
  - `memberNameIdentifier.expression.getText`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---