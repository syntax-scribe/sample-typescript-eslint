[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useDebouncedToggle.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useDebouncedToggle.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useRef` | `react` |
| `useState` | `react` |


---

## Functions

### `useDebouncedToggle(value: T, timeout: number): [T, (data: T) => void]`

<details><summary>Code</summary>

```ts
export function useDebouncedToggle<T>(
  value: T,
  timeout = 1000,
): [T, (data: T) => void] {
  const [state, setState] = useState<T>(value);
  const timeoutIdRef = useRef<NodeJS.Timeout>();

  const update = useCallback(
    (data: T) => {
      setState(data);
      const timeoutId = timeoutIdRef.current;
      if (timeoutId) {
        timeoutIdRef.current = undefined;
        clearTimeout(timeoutId);
      }
      timeoutIdRef.current = setTimeout(() => {
        setState(value);
      }, timeout);
    },
    [timeout, value],
  );

  return [state, update];
}
```
</details>

- **Parameters**:
  - `value: T`
  - `timeout: number`
- **Return Type**: `[T, (data: T) => void]`
- **Calls**:
  - `useState (from react)`
  - `useRef (from react)`
  - `useCallback (from react)`
  - `setState`
  - `clearTimeout`
  - `setTimeout`

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