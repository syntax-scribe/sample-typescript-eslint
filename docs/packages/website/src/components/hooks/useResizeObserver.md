[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `useResizeObserver.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/hooks/useResizeObserver.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useEffect` | `react` |
| `useMemo` | `react` |


---

## Functions

### `useResizeObserver(element: HTMLElement | null, callback: () => void): void`

<details><summary>Code</summary>

```ts
(
  element: HTMLElement | null,
  callback: () => void,
): void => {
  const resizeObserver = useMemo(() => {
    return new ResizeObserver(() => {
      callback();
    });
  }, [callback]);

  useEffect(() => {
    if (element) {
      resizeObserver.observe(element);
    }
    return (): void => {
      if (element) {
        resizeObserver.unobserve(element);
      }
    };
  }, [element, resizeObserver]);
}
```
</details>

- **Parameters**:
  - `element: HTMLElement | null`
  - `callback: () => void`
- **Return Type**: `void`
- **Calls**:
  - `useMemo (from react)`
  - `callback`
  - `useEffect (from react)`
  - `resizeObserver.observe`
  - `resizeObserver.unobserve`

---