[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useHistorySelector.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/hooks/useHistorySelector.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useHistory` | `@docusaurus/router` |
| `useSyncExternalStore` | `react` |


---

## Functions

### `useHistorySelector(selector: HistorySelector<T>, getServerSnapshot: () => T): T`

<details><summary>Code</summary>

```ts
export function useHistorySelector<T>(
  selector: HistorySelector<T>,
  getServerSnapshot: () => T,
): T {
  const history = useHistory();
  return useSyncExternalStore(
    history.listen,
    () => selector(history),
    getServerSnapshot,
  );
}
```
</details>

- **Parameters**:
  - `selector: HistorySelector<T>`
  - `getServerSnapshot: () => T`
- **Return Type**: `T`
- **Calls**:
  - `useHistory (from @docusaurus/router)`
  - `useSyncExternalStore (from react)`
  - `selector`

---

## Type Aliases

### `HistorySelector<T>`

```ts
type HistorySelector<T> = (history: H.History) => T;
```


---