[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `ASTViewer.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 10 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 3 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/ASTViewer.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useEffect` | `react` |
| `useMemo` | `react` |
| `React` | `react` |
| `OnHoverNodeFn` | `./types` |
| `CopyButton` | `../inputs/CopyButton` |
| `debounce` | `../lib/debounce` |
| `scrollIntoViewIfNeeded` | `../lib/scroll-into` |
| `styles` | `./ASTViewer.module.css` |
| `DataRender` | `./DataRenderer` |
| `findSelectionPath` | `./selectedRange` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.list} | <DataRender>, {!hideCopyButton && <CopyButton value={model} />} |
| `DataRender` | component | lastElement={true}, level="ast", onHover={onHoverNode}, selectedPath={selectedPath}, showTokens={showTokens}, value={model} | *none* |
| `CopyButton` | component | value={model} | *none* |


---

## Functions

### `tryToApplyFilter(value: T, filter: ESQuery.Selector): T | T[]`

<details><summary>Code</summary>

```ts
function tryToApplyFilter<T>(value: T, filter?: ESQuery.Selector): T | T[] {
  try {
    // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
    if (window.esquery && filter) {
      // @ts-expect-error - esquery requires js ast types
      return window.esquery.match(value, filter, {
        visitorKeys: window.visitorKeys,
      });
    }
  } catch (e: unknown) {
    console.error(e);
  }
  return value;
}
```
</details>

- **Parameters**:
  - `value: T`
  - `filter: ESQuery.Selector`
- **Return Type**: `T | T[]`
- **Calls**:
  - `window.esquery.match`
  - `console.error`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
// @ts-expect-error - esquery requires js ast types
```

### `ASTViewer({
  cursorPosition,
  enableScrolling,
  filter,
  hideCopyButton,
  onHoverNode,
  showTokens,
  value,
}: ASTViewerProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function ASTViewer({
  cursorPosition,
  enableScrolling,
  filter,
  hideCopyButton,
  onHoverNode,
  showTokens,
  value,
}: ASTViewerProps): React.JSX.Element {
  const model = useMemo(() => {
    if (filter) {
      return tryToApplyFilter(value, filter);
    }
    return value;
  }, [value, filter]);

  const selectedPath = useMemo(() => {
    if (cursorPosition == null || !model || typeof model !== 'object') {
      return 'ast';
    }
    return findSelectionPath(model, cursorPosition).path.join('.');
  }, [cursorPosition, model]);

  useEffect(() => {
    if (enableScrolling) {
      const delayed = debounce(() => {
        const htmlElement = document.querySelector(
          `div[data-level="${selectedPath}"] > a`,
        );
        if (htmlElement) {
          scrollIntoViewIfNeeded(htmlElement);
        }
      }, 100);
      delayed();
    }
  }, [selectedPath, enableScrolling]);

  return (
    <div className={styles.list}>
      <DataRender
        lastElement={true}
        level="ast"
        onHover={onHoverNode}
        selectedPath={selectedPath}
        showTokens={showTokens}
        value={model}
      />
      {!hideCopyButton && <CopyButton value={model} />}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  cursorPosition,
  enableScrolling,
  filter,
  hideCopyButton,
  onHoverNode,
  showTokens,
  value,
}: ASTViewerProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useMemo (from react)`
  - `tryToApplyFilter`
  - `findSelectionPath(model, cursorPosition).path.join`
  - `useEffect (from react)`
  - `debounce (from ../lib/debounce)`
  - `document.querySelector`
  - `scrollIntoViewIfNeeded (from ../lib/scroll-into)`
  - `delayed`

---

## Interfaces

### `ASTViewerProps`

<details><summary>Interface Code</summary>

```ts
export interface ASTViewerProps {
  readonly cursorPosition?: number;
  readonly enableScrolling?: boolean;
  readonly filter?: ESQuery.Selector;
  readonly hideCopyButton?: boolean;
  readonly onHoverNode?: OnHoverNodeFn;
  readonly showTokens?: boolean;
  readonly value: unknown;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `cursorPosition` | `number` | ✓ |  |
| `enableScrolling` | `boolean` | ✓ |  |
| `filter` | `ESQuery.Selector` | ✓ |  |
| `hideCopyButton` | `boolean` | ✓ |  |
| `onHoverNode` | `OnHoverNodeFn` | ✓ |  |
| `showTokens` | `boolean` | ✓ |  |
| `value` | `unknown` | ✗ |  |


---