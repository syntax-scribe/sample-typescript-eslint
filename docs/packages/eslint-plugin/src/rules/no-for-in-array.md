[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-for-in-array.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
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
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-for-in-array.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getForStatementHeadLoc` | `../util/getForStatementHeadLoc` |


---

## Functions

### `isArrayLike(checker: ts.TypeChecker, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isArrayLike(checker: ts.TypeChecker, type: ts.Type): boolean {
  return isTypeRecurser(
    type,
    t => t.getNumberIndexType() != null && hasArrayishLength(checker, t),
  );
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeRecurser`
  - `t.getNumberIndexType`
  - `hasArrayishLength`
### `hasArrayishLength(checker: ts.TypeChecker, type: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function hasArrayishLength(checker: ts.TypeChecker, type: ts.Type): boolean {
  const lengthProperty = type.getProperty('length');

  if (lengthProperty == null) {
    return false;
  }

  return tsutils.isTypeFlagSet(
    checker.getTypeOfSymbol(lengthProperty),
    ts.TypeFlags.NumberLike,
  );
}
```
</details>

- **Parameters**:
  - `checker: ts.TypeChecker`
  - `type: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `type.getProperty`
  - `tsutils.isTypeFlagSet`
  - `checker.getTypeOfSymbol`
### `isTypeRecurser(type: ts.Type, predicate: (t: ts.Type) => boolean): boolean`

<details><summary>Code</summary>

```ts
function isTypeRecurser(
  type: ts.Type,
  predicate: (t: ts.Type) => boolean,
): boolean {
  if (type.isUnionOrIntersection()) {
    return type.types.some(t => isTypeRecurser(t, predicate));
  }

  return predicate(type);
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `predicate: (t: ts.Type) => boolean`
- **Return Type**: `boolean`
- **Calls**:
  - `type.isUnionOrIntersection`
  - `type.types.some`
  - `isTypeRecurser`
  - `predicate`

---