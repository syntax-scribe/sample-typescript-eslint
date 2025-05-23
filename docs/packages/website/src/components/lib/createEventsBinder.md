[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createEventsBinder.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/createEventsBinder.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---