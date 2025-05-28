[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TypesDetails.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 8 |
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

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `PanelGroup` | component | autoSaveId="playground-types", direction="horizontal" | <Panel>, <PanelResizeHandle>, <Panel> |
| `Panel` | component | className={styles.PanelColumn}, collapsible={true}, defaultSize={35}, id="simplifiedTree" | <div> |
| `div` | element | className={styles.playgroundInfoContainer} | <SimplifiedTreeView> |
| `SimplifiedTreeView` | component | onHoverNode={onHoverNode}, onSelect={setSelectedNode}, selectedNode={selectedNode}, value={value} | *none* |
| `PanelResizeHandle` | component | className={styles.PanelResizeHandle} | *none* |
| `Panel` | component | className={styles.PanelColumn}, collapsible={true}, id="typeInfo" | <div> |
| `div` | element | className={styles.playgroundInfoContainer} | <TypeInfo> |
| `TypeInfo` | component | onHoverNode={onHoverNode}, typeChecker={typeChecker}, value={selectedNode} | *none* |


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