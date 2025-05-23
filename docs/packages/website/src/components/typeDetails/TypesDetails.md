[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TypesDetails.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 12
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/typeDetails/TypesDetails.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useEffect` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `Panel` | `react-resizable-panels` |
| `PanelGroup` | `react-resizable-panels` |
| `PanelResizeHandle` | `react-resizable-panels` |
| `OnHoverNodeFn` | `../ast/types` |
| `findSelectionPath` | `../ast/selectedRange` |
| `isTSNode` | `../ast/utils` |
| `styles` | `../Playground.module.css` |
| `SimplifiedTreeView` | `./SimplifiedTreeView` |
| `TypeInfo` | `./TypeInfo` |


---

## Functions

### `TypesDetails({
  cursorPosition,
  onHoverNode,
  typeChecker,
  value,
}: TypesDetailsProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function TypesDetails({
  cursorPosition,
  onHoverNode,
  typeChecker,
  value,
}: TypesDetailsProps): React.JSX.Element {
  const [selectedNode, setSelectedNode] = useState<ts.Node>(value);

  useEffect(() => {
    if (cursorPosition) {
      const item = findSelectionPath(value, cursorPosition);
      if (item.node && isTSNode(item.node)) {
        setSelectedNode(item.node);
      }
    }
  }, [cursorPosition, value]);

  return (
    <PanelGroup autoSaveId="playground-types" direction="horizontal">
      <Panel
        className={styles.PanelColumn}
        collapsible={true}
        defaultSize={35}
        id="simplifiedTree"
      >
        <div className={styles.playgroundInfoContainer}>
          <SimplifiedTreeView
            onHoverNode={onHoverNode}
            onSelect={setSelectedNode}
            selectedNode={selectedNode}
            value={value}
          />
        </div>
      </Panel>
      <PanelResizeHandle className={styles.PanelResizeHandle} />
      <Panel className={styles.PanelColumn} collapsible={true} id="typeInfo">
        <div className={styles.playgroundInfoContainer}>
          <TypeInfo
            onHoverNode={onHoverNode}
            typeChecker={typeChecker}
            value={selectedNode}
          />
        </div>
      </Panel>
    </PanelGroup>
  );
}
```
</details>

- **Parameters**:
  - `{
  cursorPosition,
  onHoverNode,
  typeChecker,
  value,
}: TypesDetailsProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useEffect (from react)`
  - `findSelectionPath (from ../ast/selectedRange)`
  - `isTSNode (from ../ast/utils)`
  - `setSelectedNode`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `TypesDetailsProps`

<details><summary>Interface Code</summary>

```ts
export interface TypesDetailsProps {
  readonly cursorPosition?: number;
  readonly onHoverNode?: OnHoverNodeFn;
  readonly typeChecker?: ts.TypeChecker;
  readonly value: ts.Node;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `cursorPosition` | `number` | ✓ |  |
| `onHoverNode` | `OnHoverNodeFn` | ✓ |  |
| `typeChecker` | `ts.TypeChecker` | ✓ |  |
| `value` | `ts.Node` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---