[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useBool.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useBool.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Dispatch` | `react` |
| `SetStateAction` | `react` |
| `useCallback` | `react` |
| `useState` | `react` |


---

## Functions

### `useBool(initialState: boolean | (() => boolean)): [boolean, () => void, Dispatch<SetStateAction<boolean>>]`

<details><summary>Code</summary>

```ts
export function useBool(
  initialState: boolean | (() => boolean),
): [boolean, () => void, Dispatch<SetStateAction<boolean>>] {
  const [value, setValue] = useState(initialState);

  const toggle = useCallback(
    (): void => setValue(currentValue => !currentValue),
    [],
  );

  return [value, toggle, setValue];
}
```
</details>

- **Parameters**:
  - `initialState: boolean | (() => boolean)`
- **Return Type**: `[boolean, () => void, Dispatch<SetStateAction<boolean>>]`
- **Calls**:
  - `useState (from react)`
  - `useCallback (from react)`
  - `setValue`

---