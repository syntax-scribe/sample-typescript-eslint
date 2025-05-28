[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `RuleTester.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 1 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/tests/RuleTester.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `@typescript-eslint/rule-tester` | RuleTester |


---

## Functions

### `getFixturesRootDir(): string`

<details><summary>Code</summary>

```ts
export function getFixturesRootDir(): string {
  return path.join(__dirname, 'fixtures');
}
```
</details>

- **Return Type**: `string`
- **Calls**:
  - `path.join`

---