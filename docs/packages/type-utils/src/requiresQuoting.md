[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `requiresQuoting.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |

## 📚 Table of Contents

- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/src/requiresQuoting.ts`**

## Functions

### `requiresQuoting(name: string, target: ts.ScriptTarget): boolean`

<details><summary>Code</summary>

```ts
export function requiresQuoting(
  name: string,
  target: ts.ScriptTarget = ts.ScriptTarget.ESNext,
): boolean {
  if (name.length === 0) {
    return true;
  }

  if (!ts.isIdentifierStart(name.charCodeAt(0), target)) {
    return true;
  }

  for (let i = 1; i < name.length; i += 1) {
    if (!ts.isIdentifierPart(name.charCodeAt(i), target)) {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/*** Indicates whether identifiers require the use of quotation marks when accessing property definitions and dot notation. */
```

- **Parameters**:
  - `name: string`
  - `target: ts.ScriptTarget`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isIdentifierStart`
  - `name.charCodeAt`
  - `ts.isIdentifierPart`

---