[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ID.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/ID.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ID_CACHE` | `Map<number, number>` | const | `new Map<number, number>()` | ✗ |
| `NEXT_KEY` | `number` | let/var | `0` | ✗ |
| `key` | `number` | const | `(NEXT_KEY += 1)` | ✗ |
| `current` | `number` | const | `ID_CACHE.get(key) ?? 0` | ✗ |
| `next` | `number` | const | `current + 1` | ✗ |


---

## Functions

### `createIdGenerator(): () => number`

<details><summary>Code</summary>

```ts
export function createIdGenerator(): () => number {
  const key = (NEXT_KEY += 1);
  ID_CACHE.set(key, 0);

  return (): number => {
    const current = ID_CACHE.get(key) ?? 0;
    const next = current + 1;
    ID_CACHE.set(key, next);
    return next;
  };
}
```
</details>

- **Return Type**: `() => number`
- **Calls**:
  - `ID_CACHE.set`
  - `ID_CACHE.get`
### `resetIds(): void`

<details><summary>Code</summary>

```ts
export function resetIds(): void {
  ID_CACHE.clear();
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `ID_CACHE.clear`

---