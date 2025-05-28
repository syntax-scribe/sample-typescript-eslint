[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useDebouncedToggle.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
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

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useDebouncedToggle.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useRef` | `react` |
| `useState` | `react` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `timeoutId` | `any` | const | `timeoutIdRef.current` | ✗ |


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