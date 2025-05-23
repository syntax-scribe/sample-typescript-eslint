[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `dedupeTestCases.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/dedupeTestCases.ts`**

## 📦 Imports

> No imports found in this file.


---

## Functions

### `dedupeTestCases(caseArrays: (readonly T[])[]): T[]`

<details><summary>Code</summary>

```ts
<T>(...caseArrays: (readonly T[])[]): T[] => {
  const cases = caseArrays.flat();
  const dedupedCases = Object.values(
    Object.fromEntries(
      cases.map(testCase => [JSON.stringify(testCase), testCase]),
    ),
  );
  if (cases.length === dedupedCases.length) {
    throw new Error(
      '`dedupeTestCases` is not necessary — no duplicate test cases detected!',
    );
  }
  return dedupedCases;
}
```
</details>

- **Parameters**:
  - `caseArrays: (readonly T[])[]`
- **Return Type**: `T[]`
- **Calls**:
  - `caseArrays.flat`
  - `Object.values`
  - `Object.fromEntries`
  - `cases.map`
  - `JSON.stringify`

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