[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `fixture.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

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