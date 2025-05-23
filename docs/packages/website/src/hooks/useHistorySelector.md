[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useHistorySelector.ts`

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `HistorySelector<T>`

```ts
type HistorySelector<T> = (history: H.History) => T;
```


---