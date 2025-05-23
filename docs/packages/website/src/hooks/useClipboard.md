[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useClipboard.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useClipboard.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useDebouncedToggle` | `./useDebouncedToggle` |


---

## Functions

### `useClipboard(code: () => string): useClipboardResult`

<details><summary>Code</summary>

```ts
export function useClipboard(code: () => string): useClipboardResult {
  const [copied, setCopied] = useDebouncedToggle(false);

  const copy = useCallback(
    () =>
      navigator.clipboard.writeText(code()).then(() => {
        setCopied(true);
      }),
    [setCopied, code],
  );

  return [copied, copy];
}
```
</details>

- **Parameters**:
  - `code: () => string`
- **Return Type**: `useClipboardResult`
- **Calls**:
  - `useDebouncedToggle (from ./useDebouncedToggle)`
  - `useCallback (from react)`
  - `navigator.clipboard.writeText(code()).then`
  - `setCopied`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `useClipboardResult`

```ts
type useClipboardResult = [copied: boolean, copy: () => void];
```


---