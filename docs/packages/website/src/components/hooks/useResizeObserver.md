[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `useResizeObserver.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---