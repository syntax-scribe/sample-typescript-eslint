[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `needsToBeAwaited.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/needsToBeAwaited.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isTypeAnyType` | `@typescript-eslint/type-utils` |
| `isTypeUnknownType` | `@typescript-eslint/type-utils` |
| `getConstraintInfo` | `./getConstraintInfo` |


---

## Functions

### `needsToBeAwaited(checker: ts.TypeChecker, node: ts.Node, type: ts.Type): Awaitable`

<details><summary>Code</summary>

```ts
export function needsToBeAwaited(
  checker: ts.TypeChecker,
  node: ts.Node,
  type: ts.Type,
): Awaitable {
  const { constraintType, isTypeParameter } = getConstraintInfo(checker, type);

  // unconstrained generic types should be treated as unknown
  if (isTypeParameter && constraintType == null) {
    return Awaitable.May;
  }

  // `any` and `unknown` types may need to be awaited
  if (isTypeAnyType(constraintType) || isTypeUnknownType(constraintType)) {
    return Awaitable.May;
  }

  // 'thenable' values should always be be awaited
  if (tsutils.isThenableType(checker, node, constraintType)) {
    return Awaitable.Always;
  }

  // anything else should not be awaited
  return Awaitable.Never;
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `node: ts.Node`
  - `type: ts.Type`
- **Return Type**: `Awaitable`
- **Calls**:
  - `getConstraintInfo (from ./getConstraintInfo)`
  - `isTypeAnyType (from @typescript-eslint/type-utils)`
  - `isTypeUnknownType (from @typescript-eslint/type-utils)`
  - `tsutils.isThenableType`
- **Internal Comments**:
```
// unconstrained generic types should be treated as unknown
// `any` and `unknown` types may need to be awaited
// 'thenable' values should always be be awaited
// anything else should not be awaited
```


---

## Enums

### `enum Awaitable`

<details><summary>Enum Code</summary>

```ts
export enum Awaitable {
  Always,
  Never,
  May,
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Always` | *auto* |  |
| `Never` | *auto* |  |
| `May` | *auto* |  |


---