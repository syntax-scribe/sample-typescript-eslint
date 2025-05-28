[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getConstraintInfo.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getConstraintInfo.ts`**

## Functions

### `getConstraintInfo(checker: ts.TypeChecker, type: ts.Type): ConstraintTypeInfo`

<details><summary>Code</summary>

```ts
export function getConstraintInfo(
  checker: ts.TypeChecker,
  type: ts.Type,
): ConstraintTypeInfo {
  if (tsutils.isTypeParameter(type)) {
    const constraintType = checker.getBaseConstraintOfType(type);
    return {
      constraintType,
      isTypeParameter: true,
    };
  }
  return {
    constraintType: type,
    isTypeParameter: false,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns whether the type is a generic and what its constraint is.
 *
 * If the type is not a generic, `isTypeParameter` will be `false`, and
 * `constraintType` will be the same as the input type.
 *
 * If the type is a generic, and it is constrained, `isTypeParameter` will be
 * `true`, and `constraintType` will be the constraint type.
 *
 * If the type is a generic, but it is not constrained, `constraintType` will be
 * `undefined` (rather than an `unknown` type), due to https://github.com/microsoft/TypeScript/issues/60475
 *
 * Successor to {@link getConstrainedTypeAtLocation} due to https://github.com/typescript-eslint/typescript-eslint/issues/10438
 *
 * This is considered internal since it is unstable for now and may have breaking changes at any time.
 * Use at your own risk.
 *
 * @internal
 *
 */
```

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `ConstraintTypeInfo`
- **Calls**:
  - `tsutils.isTypeParameter`
  - `checker.getBaseConstraintOfType`

---

## Interfaces

### `ConstraintTypeInfoUnconstrained`

<details><summary>Interface Code</summary>

```ts
export interface ConstraintTypeInfoUnconstrained {
  constraintType: undefined;
  isTypeParameter: true;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `constraintType` | `undefined` | ✗ |  |
| `isTypeParameter` | `true` | ✗ |  |

### `ConstraintTypeInfoConstrained`

<details><summary>Interface Code</summary>

```ts
export interface ConstraintTypeInfoConstrained {
  constraintType: ts.Type;
  isTypeParameter: true;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `constraintType` | `ts.Type` | ✗ |  |
| `isTypeParameter` | `true` | ✗ |  |

### `ConstraintTypeInfoNonGeneric`

<details><summary>Interface Code</summary>

```ts
export interface ConstraintTypeInfoNonGeneric {
  constraintType: ts.Type;
  isTypeParameter: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `constraintType` | `ts.Type` | ✗ |  |
| `isTypeParameter` | `false` | ✗ |  |


---

## Type Aliases

### `ConstraintTypeInfo`

```ts
type ConstraintTypeInfo = | ConstraintTypeInfoConstrained
  | ConstraintTypeInfoNonGeneric
  | ConstraintTypeInfoUnconstrained;
```


---