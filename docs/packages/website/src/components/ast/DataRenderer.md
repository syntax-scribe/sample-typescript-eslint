[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `DataRenderer.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 6 |
| 🧱 Classes | 0 |
| 📦 Imports | 19 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 25 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/DataRenderer.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `useCallback` | `react` |
| `useEffect` | `react` |
| `useMemo` | `react` |
| `React` | `react` |
| `OnHoverNodeFn` | `./types` |
| `ParentNodeType` | `./types` |
| `useBool` | `../../hooks/useBool` |
| `Tooltip` | `../inputs/Tooltip` |
| `styles` | `./ASTViewer.module.css` |
| `HiddenItem` | `./HiddenItem` |
| `PropertyName` | `./PropertyName` |
| `PropertyValue` | `./PropertyValue` |
| `filterProperties` | `./utils` |
| `getNodeType` | `./utils` |
| `getRange` | `./utils` |
| `getTooltipLabel` | `./utils` |
| `getTypeName` | `./utils` |
| `isRecord` | `./utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `shouldOpen` | `boolean` | const | `!!selectedPath?.startsWith(level)` | ✗ |
| `lastIndex` | `number` | const | `data.length - 1` | ✗ |
| `value` | `unknown` | const | `props.value` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={clsx(
        styles.expand,
        !expanded && styles.open,
        isActive && styles.selected,
      )}, data-level={level}, role="list" | {field && (
        <PropertyName
          className={styles.propName}
          onClick={toggleExpanded}
          onHover={onHoverItem}
          value={field}
        />
      )}, {field && <span>: </span>}, {typeName && (
        <PropertyName
          className={styles.tokenName}
          onClick={toggleExpanded}
          onHover={onHoverItem}
          value={typeName}
        />
      )}, {typeName && <span> </span>}, <span>, {expanded ? (
        <div className={styles.subList}>
          {data.map((dataElement, index) => (
            <DataRender
              field={dataElement[0]}
              key={dataElement[0]}
              lastElement={index === lastIndex}
              level={`${level}.${dataElement[0]}`}
              nodeType={nodeType}
              onHover={onHover}
              selectedPath={selectedPath}
              showTokens={showTokens}
              value={dataElement[1]}
            />
          ))}
        </div>
      ) : (
        <HiddenItem isArray={openBracket === '['} level={level} value={data} />
      )}, <span>, {!lastElement && <span>,</span>} |
| `PropertyName` | component | className={styles.propName}, onClick={toggleExpanded}, onHover={onHoverItem}, value={field} | *none* |
| `span` | element | *none* | text: ":" |
| `PropertyName` | component | className={styles.tokenName}, onClick={toggleExpanded}, onHover={onHoverItem}, value={typeName} | *none* |
| `span` | element | *none* | *none* |
| `span` | element | *none* | {openBracket} |
| `div` | element | className={styles.subList} | {data.map((dataElement, index) => (
            <DataRender
              field={dataElement[0]}
              key={dataElement[0]}
              lastElement={index === lastIndex}
              level={`${level}.${dataElement[0]}`}
              nodeType={nodeType}
              onHover={onHover}
              selectedPath={selectedPath}
              showTokens={showTokens}
              value={dataElement[1]}
            />
          ))} |
| `DataRender` | component | field={dataElement[0]}, key={dataElement[0]}, lastElement={index === lastIndex}, level={`${level}.${dataElement[0]}`}, nodeType={nodeType}, onHover={onHover}, selectedPath={selectedPath}, showTokens={showTokens}, value={dataElement[1]} | *none* |
| `HiddenItem` | component | isArray={openBracket === '['}, level={level}, value={data} | *none* |
| `span` | element | *none* | {closeBracket} |
| `span` | element | *none* | text: "," |
| `RenderExpandableObject` | component | closeBracket="}", data={computed.value}, nodeType={computed.nodeType}, openBracket="{", typeName={computed.typeName} | *none* |
| `RenderExpandableObject` | component | closeBracket="]", data={Object.entries(props.value)}, openBracket="[" | *none* |
| `RenderExpandableObject` | component | closeBracket=")", data={Object.entries(props.value)}, openBracket="(" | *none* |
| `div` | element | className={styles.valueBody}, role="listitem" | {field && <span className={styles.propName}>{field}: </span>}, {tooltip ? (
        <Tooltip hover={true} position="right" text={tooltip}>
          <PropertyValue value={value} />
        </Tooltip>
      ) : (
        <PropertyValue value={value} />
      )}, {!lastElement && <span className={styles.label}>,</span>} |
| `span` | element | className={styles.propName} | {field}, text: ":" |
| `Tooltip` | component | hover={true}, position="right", text={tooltip} | <PropertyValue> |
| `PropertyValue` | component | value={value} | *none* |
| `PropertyValue` | component | value={value} | *none* |
| `span` | element | className={styles.label} | text: "," |
| `JsonArray` | component | value={value} | *none* |
| `JsonObject` | component | value={value} | *none* |
| `JsonIterable` | component | typeName="Map", value={value} | *none* |
| `JsonIterable` | component | typeName="Set", value={value} | *none* |
| `JsonPrimitiveValue` | component | *none* | *none* |


---

## Functions

### `RenderExpandableObject({
  closeBracket,
  data,
  field,
  lastElement,
  level,
  nodeType,
  onHover,
  openBracket,
  selectedPath,
  showTokens,
  typeName,
  value,
}: ExpandableRenderProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function RenderExpandableObject({
  closeBracket,
  data,
  field,
  lastElement,
  level,
  nodeType,
  onHover,
  openBracket,
  selectedPath,
  showTokens,
  typeName,
  value,
}: ExpandableRenderProps): React.JSX.Element {
  const [expanded, toggleExpanded, setExpanded] = useBool(
    () => level === 'ast' || !!selectedPath?.startsWith(level),
  );

  const isActive = useMemo(
    () => level !== 'ast' && selectedPath === level,
    [selectedPath, level],
  );

  const onHoverItem = useCallback(
    (hover: boolean): void => {
      if (onHover) {
        if (hover) {
          onHover(getRange(value, nodeType));
        } else {
          onHover(undefined);
        }
      }
    },
    [onHover, value, nodeType],
  );

  useEffect(() => {
    const shouldOpen = !!selectedPath?.startsWith(level);
    if (shouldOpen) {
      setExpanded(current => current || shouldOpen);
    }
  }, [selectedPath, level, setExpanded]);

  const lastIndex = data.length - 1;

  return (
    <div
      className={clsx(
        styles.expand,
        !expanded && styles.open,
        isActive && styles.selected,
      )}
      data-level={level}
      role="list"
    >
      {field && (
        <PropertyName
          className={styles.propName}
          onClick={toggleExpanded}
          onHover={onHoverItem}
          value={field}
        />
      )}
      {field && <span>: </span>}
      {typeName && (
        <PropertyName
          className={styles.tokenName}
          onClick={toggleExpanded}
          onHover={onHoverItem}
          value={typeName}
        />
      )}
      {typeName && <span> </span>}
      <span>{openBracket}</span>

      {expanded ? (
        <div className={styles.subList}>
          {data.map((dataElement, index) => (
            <DataRender
              field={dataElement[0]}
              key={dataElement[0]}
              lastElement={index === lastIndex}
              level={`${level}.${dataElement[0]}`}
              nodeType={nodeType}
              onHover={onHover}
              selectedPath={selectedPath}
              showTokens={showTokens}
              value={dataElement[1]}
            />
          ))}
        </div>
      ) : (
        <HiddenItem isArray={openBracket === '['} level={level} value={data} />
      )}

      <span>{closeBracket}</span>
      {!lastElement && <span>,</span>}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  closeBracket,
  data,
  field,
  lastElement,
  level,
  nodeType,
  onHover,
  openBracket,
  selectedPath,
  showTokens,
  typeName,
  value,
}: ExpandableRenderProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useBool (from ../../hooks/useBool)`
  - `selectedPath?.startsWith`
  - `useMemo (from react)`
  - `useCallback (from react)`
  - `onHover`
  - `getRange (from ./utils)`
  - `useEffect (from react)`
  - `setExpanded`
  - `clsx (from clsx)`
  - `data.map`
### `JsonObject(props: JsonRenderProps<Record<string, unknown>>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function JsonObject(
  props: JsonRenderProps<Record<string, unknown>>,
): React.JSX.Element {
  const computed = useMemo(() => {
    const nodeType = getNodeType(props.value);
    return {
      nodeType,
      typeName: getTypeName(props.value, nodeType),
      value: Object.entries(props.value).filter(item =>
        filterProperties(item[0], item[1], nodeType, props.showTokens),
      ),
    };
  }, [props.value, props.showTokens]);

  return (
    <RenderExpandableObject
      {...props}
      closeBracket="}"
      data={computed.value}
      nodeType={computed.nodeType}
      openBracket="{"
      typeName={computed.typeName}
    />
  );
}
```
</details>

- **Parameters**:
  - `props: JsonRenderProps<Record<string, unknown>>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useMemo (from react)`
  - `getNodeType (from ./utils)`
  - `getTypeName (from ./utils)`
  - `Object.entries(props.value).filter`
  - `filterProperties (from ./utils)`
### `JsonArray(props: JsonRenderProps<unknown[]>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function JsonArray(props: JsonRenderProps<unknown[]>): React.JSX.Element {
  return (
    <RenderExpandableObject
      {...props}
      closeBracket="]"
      data={Object.entries(props.value)}
      openBracket="["
    />
  );
}
```
</details>

- **Parameters**:
  - `props: JsonRenderProps<unknown[]>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `Object.entries`
### `JsonIterable(props: JsonRenderProps<Iterable<unknown>>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function JsonIterable(
  props: JsonRenderProps<Iterable<unknown>>,
): React.JSX.Element {
  return (
    <RenderExpandableObject
      {...props}
      closeBracket=")"
      data={Object.entries(props.value)}
      openBracket="("
    />
  );
}
```
</details>

- **Parameters**:
  - `props: JsonRenderProps<Iterable<unknown>>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `Object.entries`
### `JsonPrimitiveValue({
  field,
  lastElement,
  nodeType,
  value,
}: JsonRenderProps<unknown>): React.JSX.Element`

<details><summary>Code</summary>

```ts
function JsonPrimitiveValue({
  field,
  lastElement,
  nodeType,
  value,
}: JsonRenderProps<unknown>): React.JSX.Element {
  const tooltip = useMemo(() => {
    if (field && nodeType) {
      return getTooltipLabel(value, field, nodeType);
    }
    return undefined;
  }, [value, field, nodeType]);

  return (
    <div className={styles.valueBody} role="listitem">
      {field && <span className={styles.propName}>{field}: </span>}
      {tooltip ? (
        <Tooltip hover={true} position="right" text={tooltip}>
          <PropertyValue value={value} />
        </Tooltip>
      ) : (
        <PropertyValue value={value} />
      )}
      {!lastElement && <span className={styles.label}>,</span>}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  field,
  lastElement,
  nodeType,
  value,
}: JsonRenderProps<unknown>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useMemo (from react)`
  - `getTooltipLabel (from ./utils)`
### `DataRender(props: JsonRenderProps<unknown>): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function DataRender(
  props: JsonRenderProps<unknown>,
): React.JSX.Element {
  const value = props.value;

  if (Array.isArray(value)) {
    return <JsonArray {...props} value={value} />;
  }

  if (isRecord(value)) {
    return <JsonObject {...props} value={value} />;
  }

  if (value instanceof Map) {
    return <JsonIterable typeName="Map" {...props} value={value} />;
  }

  if (value instanceof Set) {
    return <JsonIterable typeName="Set" {...props} value={value} />;
  }

  return <JsonPrimitiveValue {...props} />;
}
```
</details>

- **Parameters**:
  - `props: JsonRenderProps<unknown>`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `Array.isArray`
  - `isRecord (from ./utils)`

---

## Interfaces

### `JsonRenderProps<T>`

<details><summary>Interface Code</summary>

```ts
export interface JsonRenderProps<T> {
  readonly field?: string;
  readonly lastElement?: boolean;
  readonly level: string;
  readonly nodeType?: ParentNodeType;
  readonly onHover?: OnHoverNodeFn;
  readonly selectedPath?: string;
  readonly showTokens?: boolean;
  readonly typeName?: string;
  readonly value: T;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `field` | `string` | ✓ |  |
| `lastElement` | `boolean` | ✓ |  |
| `level` | `string` | ✗ |  |
| `nodeType` | `ParentNodeType` | ✓ |  |
| `onHover` | `OnHoverNodeFn` | ✓ |  |
| `selectedPath` | `string` | ✓ |  |
| `showTokens` | `boolean` | ✓ |  |
| `typeName` | `string` | ✓ |  |
| `value` | `T` | ✗ |  |

### `ExpandableRenderProps`

<details><summary>Interface Code</summary>

```ts
export interface ExpandableRenderProps
  extends JsonRenderProps<object | unknown[]> {
  readonly closeBracket: string;
  readonly data: [string, unknown][];
  readonly openBracket: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `closeBracket` | `string` | ✗ |  |
| `data` | `[string, unknown][]` | ✗ |  |
| `openBracket` | `string` | ✗ |  |


---