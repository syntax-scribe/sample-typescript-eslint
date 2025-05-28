[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

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
📂 **`packages/ast-spec/src/legacy-fixtures/basics/fixtures/optional-chain-call/fixture.ts`**

## Functions

### `processOptionalCall(one: any): void`

<details><summary>Code</summary>

```ts
function processOptionalCall(one?: any) {
  one?.fn();
  one?.two.fn();
  one.two?.fn();
  one.two?.three.fn();
  one.two?.three?.fn();

  one?.();
  one?.()();
  one?.()?.();

  one?.().two;
}
```
</details>

- **Parameters**:
  - `one: any`
- **Return Type**: `void`
- **Calls**:
  - `one?.fn`
  - `one?.two.fn`
  - `one.two?.fn`
  - `one.two?.three.fn`
  - `one.two?.three?.fn`
  - `one`
  - `complex_call_223`
  - `complex_call_236`

---