[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `SimplifiedTreeView.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 7 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/typeDetails/SimplifiedTreeView.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `useCallback` | `react` |
| `useMemo` | `react` |
| `React` | `react` |
| `OnHoverNodeFn` | `../ast/types` |
| `styles` | `../ast/ASTViewer.module.css` |
| `PropertyName` | `../ast/PropertyName` |
| `tsEnumToString` | `../ast/tsUtils` |
| `getRange` | `../ast/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `result` | `ts.Node[]` | const | `[]` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.nonExpand} | <span>, <div> |
| `span` | element | className={selectedNode === value ? styles.selected : ''} | <PropertyName> |
| `PropertyName` | component | className={styles.propName}, onClick={(): void => {
            onSelect(value);
          }}, onHover={onHover}, value={tsEnumToString('SyntaxKind', value.kind)} | *none* |
| `div` | element | className={clsx(styles.subList, 'padding-left--md')} | {items.map((item, index) => (
          <SimplifiedItem
            key={index.toString()}
            onHoverNode={onHoverNode}
            onSelect={onSelect}
            selectedNode={selectedNode}
            value={item}
          />
        ))} |
| `SimplifiedItem` | component | key={index.toString()}, onHoverNode={onHoverNode}, onSelect={onSelect}, selectedNode={selectedNode}, value={item} | *none* |
| `div` | element | className={clsx(styles.list, 'padding-left--sm')} | <SimplifiedItem> |
| `SimplifiedItem` | component | *none* | *none* |


---

## Functions

### `SimplifiedItem({
  onHoverNode,
  onSelect,
  selectedNode,
  value,
}: SimplifiedTreeViewProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function SimplifiedItem({
  onHoverNode,
  onSelect,
  selectedNode,
  value,
}: SimplifiedTreeViewProps): React.JSX.Element {
  const items = useMemo(() => {
    const result: ts.Node[] = [];
    value.forEachChild(child => {
      result.push(child);
    });
    return result;
  }, [value]);

  const onHover = useCallback(
    (v: boolean) => {
      if (onHoverNode) {
        return onHoverNode(v ? getRange(value, 'tsNode') : undefined);
      }
    },
    [onHoverNode, value],
  );

  return (
    <div className={styles.nonExpand}>
      <span className={selectedNode === value ? styles.selected : ''}>
        <PropertyName
          className={styles.propName}
          onClick={(): void => {
            onSelect(value);
          }}
          onHover={onHover}
          value={tsEnumToString('SyntaxKind', value.kind)}
        />
      </span>

      <div className={clsx(styles.subList, 'padding-left--md')}>
        {items.map((item, index) => (
          <SimplifiedItem
            key={index.toString()}
            onHoverNode={onHoverNode}
            onSelect={onSelect}
            selectedNode={selectedNode}
            value={item}
          />
        ))}
      </div>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  onHoverNode,
  onSelect,
  selectedNode,
  value,
}: SimplifiedTreeViewProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useMemo (from react)`
  - `value.forEachChild`
  - `result.push`
  - `useCallback (from react)`
  - `onHoverNode`
  - `getRange (from ../ast/utils)`
  - `onSelect`
  - `tsEnumToString (from ../ast/tsUtils)`
  - `clsx (from clsx)`
  - `items.map`
  - `index.toString`
### `SimplifiedTreeView(params: SimplifiedTreeViewProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function SimplifiedTreeView(
  params: SimplifiedTreeViewProps,
): React.JSX.Element {
  return (
    <div className={clsx(styles.list, 'padding-left--sm')}>
      <SimplifiedItem {...params} />
    </div>
  );
}
```
</details>

- **Parameters**:
  - `params: SimplifiedTreeViewProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `clsx (from clsx)`

---

## Interfaces

### `SimplifiedTreeViewProps`

<details><summary>Interface Code</summary>

```ts
export interface SimplifiedTreeViewProps {
  readonly onHoverNode?: OnHoverNodeFn;
  readonly onSelect: (value: ts.Node) => void;
  readonly selectedNode: ts.Node | undefined;
  readonly value: ts.Node;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `onHoverNode` | `OnHoverNodeFn` | ✓ |  |
| `onSelect` | `(value: ts.Node) => void` | ✗ |  |
| `selectedNode` | `ts.Node | undefined` | ✗ |  |
| `value` | `ts.Node` | ✗ |  |


---