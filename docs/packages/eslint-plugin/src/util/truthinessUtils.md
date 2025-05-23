[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `truthinessUtils.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/truthinessUtils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `getValueOfLiteralType` | `./getValueOfLiteralType` |


---

## Functions

### `isTruthyLiteral(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(type: ts.Type): boolean =>
  tsutils.isTrueLiteralType(type) ||
  (type.isLiteral() && !!getValueOfLiteralType(type))
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
### `isPossiblyFalsy(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(type: ts.Type): boolean =>
  tsutils
    .unionConstituents(type)
    // Intersections like `string & {}` can also be possibly falsy,
    // requiring us to look into the intersection.
    .flatMap(type => tsutils.intersectionConstituents(type))
    // PossiblyFalsy flag includes literal values, so exclude ones that
    // are definitely truthy
    .filter(t => !isTruthyLiteral(t))
    .some(type => tsutils.isTypeFlagSet(type, ts.TypeFlags.PossiblyFalsy))
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
    .unionConstituents(type)
    // Intersections like `string & {}` can also be possibly falsy,
    // requiring us to look into the intersection.
    .flatMap(type => tsutils.intersectionConstituents(type))
    // PossiblyFalsy flag includes literal values, so exclude ones that
    // are definitely truthy
    .filter(t => !isTruthyLiteral(t))
    .some`
### `isPossiblyTruthy(type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
(type: ts.Type): boolean =>
  tsutils
    .unionConstituents(type)
    .map(type => tsutils.intersectionConstituents(type))
    .some(intersectionParts =>
      // It is possible to define intersections that are always falsy,
      // like `"" & { __brand: string }`.
      intersectionParts.every(type => !tsutils.isFalsyType(type)),
    )
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `tsutils
    .unionConstituents(type)
    .map(type => tsutils.intersectionConstituents(type))
    .some`

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