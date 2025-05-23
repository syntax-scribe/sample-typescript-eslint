[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `restrict-template-expressions.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 15
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/restrict-template-expressions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `Type` | `typescript` |
| `TypeChecker` | `typescript` |
| `typeMatchesSomeSpecifier` | `@typescript-eslint/type-utils` |
| `typeOrValueSpecifiersSchema` | `@typescript-eslint/type-utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TypeFlags` | `typescript` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getTypeName` | `../util` |
| `isTypeAnyType` | `../util` |
| `isTypeFlagSet` | `../util` |
| `isTypeNeverType` | `../util` |


---

## Functions

### `testTypeFlag(flagsToCheck: TypeFlags): OptionTester`

<details><summary>Code</summary>

```ts
(flagsToCheck: TypeFlags): OptionTester =>
  type =>
    isTypeFlagSet(type, flagsToCheck)
```
</details>

- **Parameters**:
  - `flagsToCheck: TypeFlags`
- **Return Type**: `OptionTester`
### `recursivelyCheckType(innerType: Type): boolean`

<details><summary>Code</summary>

```ts
function recursivelyCheckType(innerType: Type): boolean {
      if (innerType.isUnion()) {
        return innerType.types.every(recursivelyCheckType);
      }

      if (innerType.isIntersection()) {
        return innerType.types.some(recursivelyCheckType);
      }

      return (
        isTypeFlagSet(innerType, TypeFlags.StringLike) ||
        typeMatchesSomeSpecifier(innerType, allow, program) ||
        enabledOptionTesters.some(({ tester }) =>
          tester(innerType, checker, recursivelyCheckType),
        )
      );
    }
```
</details>

- **Parameters**:
  - `innerType: Type`
- **Return Type**: `boolean`
- **Calls**:
  - `innerType.isUnion`
  - `innerType.types.every`
  - `innerType.isIntersection`
  - `innerType.types.some`
  - `isTypeFlagSet (from ../util)`
  - `typeMatchesSomeSpecifier (from @typescript-eslint/type-utils)`
  - `enabledOptionTesters.some`
  - `tester`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `OptionTester`

```ts
type OptionTester = (
  type: Type,
  checker: TypeChecker,
  recursivelyCheckType: (type: Type) => boolean,
) => boolean;
```

### `Options`

```ts
type Options = [
  {
    allow?: TypeOrValueSpecifier[];
  } & Partial<Record<(typeof optionTesters)[number]['option'], boolean>>,
];
```

### `MessageId`

```ts
type MessageId = 'invalidType';
```


---