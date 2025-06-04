[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `serialization.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/serialization.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `valAsObj` | `Record<string, unknown>` | const | `val as Record<string, unknown>` | ✗ |


---

## Functions

### `isSerializablePrimitiveOrPlainObject(val: unknown): boolean`

<details><summary>Code</summary>

```ts
function isSerializablePrimitiveOrPlainObject(val: unknown): boolean {
  return (
    // eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish
    val === null ||
    typeof val === 'string' ||
    typeof val === 'boolean' ||
    typeof val === 'number' ||
    (typeof val === 'object' && val.constructor === Object) ||
    Array.isArray(val)
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a value is a primitive or plain object created by the Object constructor.
 */
```

- **Parameters**:
  - `val: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `Array.isArray`
- **Internal Comments**:
```
// eslint-disable-next-line eqeqeq, @typescript-eslint/internal/eqeq-nullish (x7)
```

### `isSerializable(val: unknown): boolean`

<details><summary>Code</summary>

```ts
export function isSerializable(val: unknown): boolean {
  if (!isSerializablePrimitiveOrPlainObject(val)) {
    return false;
  }
  if (typeof val === 'object') {
    const valAsObj = val as Record<string, unknown>;
    for (const property in valAsObj) {
      if (Object.hasOwn(valAsObj, property)) {
        if (!isSerializablePrimitiveOrPlainObject(valAsObj[property])) {
          return false;
        }
        if (
          typeof valAsObj[property] === 'object' &&
          !isSerializable(valAsObj[property])
        ) {
          return false;
        }
      }
    }
  }
  return true;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Check if a value is serializable.
 * Functions or objects like RegExp cannot be serialized by JSON.stringify().
 * Inspired by: https://stackoverflow.com/questions/30579940/reliable-way-to-check-if-objects-is-serializable-in-javascript
 */
```

- **Parameters**:
  - `val: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `isSerializablePrimitiveOrPlainObject`
  - `Object.hasOwn`
  - `isSerializable`

---