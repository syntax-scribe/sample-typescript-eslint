[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `dedupeTestCases.ts`

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
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/dedupeTestCases.ts`**

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