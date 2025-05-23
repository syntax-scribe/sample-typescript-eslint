[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `requiresQuoting.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/requiresQuoting.ts`**

## 📦 Imports

> No imports found in this file.


---

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---