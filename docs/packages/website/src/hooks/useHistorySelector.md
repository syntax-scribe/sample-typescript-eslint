[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `useHistorySelector.ts`

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
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

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