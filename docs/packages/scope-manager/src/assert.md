[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `assert.ts`

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
📂 **`packages/scope-manager/src/assert.ts`**

## Functions

### `assert(value: unknown, message: string): asserts value`

<details><summary>Code</summary>

```ts
export function assert(value: unknown, message?: string): asserts value {
  if (value == null) {
    throw new Error(message);
  }
}
```
</details>

- **Parameters**:
  - `value: unknown`
  - `message: string`
- **Return Type**: `asserts value`

---