[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createEventsBinder.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
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
📂 **`packages/website/src/components/lib/createEventsBinder.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `events` | `Set<T>` | const | `new Set<T>()` | ✗ |


---

## Functions

### `createEventsBinder(): {
  register: (cb: T) => () => void;
  trigger: (...args: Parameters<T>) => void;
}`

<details><summary>Code</summary>

```ts
export function createEventsBinder<T extends (...args: any[]) => void>(): {
  register: (cb: T) => () => void;
  trigger: (...args: Parameters<T>) => void;
} {
  const events = new Set<T>();

  return {
    register(cb: T): () => void {
      events.add(cb);
      return (): void => {
        events.delete(cb);
      };
    },
    trigger(...args: Parameters<T>): void {
      events.forEach(cb => cb(...args));
    },
  };
}
```
</details>

- **Return Type**: `{
  register: (cb: T) => () => void;
  trigger: (...args: Parameters<T>) => void;
}`
- **Calls**:
  - `events.add`
  - `events.delete`
  - `events.forEach`
  - `cb`

---