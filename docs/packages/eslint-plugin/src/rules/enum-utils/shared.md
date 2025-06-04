[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `shared.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/enum-utils/shared.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isTypeFlagSet` | `../../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `symbol` | `any` | const | `type.getSymbol()!` | ✗ |
| `memberDeclaration` | `ts.EnumMember` | const | `symbol.valueDeclaration as ts.EnumMember` | ✗ |
| `enumDeclaration` | `any` | const | `memberDeclaration.parent` | ✗ |
| `memberNameIdentifier` | `any` | const | `memberDeclaration.name` | ✗ |
| `enumName` | `any` | const | `enumDeclaration.name.text` | ✗ |


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