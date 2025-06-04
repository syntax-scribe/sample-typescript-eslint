[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useClipboard.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| ⚡ Async/Await Patterns | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useClipboard.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useCallback` | `react` |
| `useDebouncedToggle` | `./useDebouncedToggle` |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| promise-chain | `useClipboard` | *none* | navigator.clipboard.writeText(code()).then |


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

## Type Aliases

### `useClipboardResult`

```ts
type useClipboardResult = [copied: boolean, copy: () => void];
```


---