[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TypeInfo.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 1 |
| 💠 JSX Elements | 20 |
| 📐 Interfaces | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/typeDetails/TypeInfo.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useMemo` | `react` |
| `React` | `react` |
| `OnHoverNodeFn` | `../ast/types` |
| `ASTViewer` | `../ast/ASTViewer` |
| `astStyles` | `../ast/ASTViewer.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `info` | `InfoModel` | const | `{}` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={astStyles.list} | <span>, <span>, <span> |
| `span` | element | className={astStyles.propClass} | {props.label} |
| `span` | element | *none* | text: ":" |
| `span` | element | className={astStyles.propString} | {String(props.value)} |
| `Fragment` | fragment | *none* | <h4> |
| `h4` | element | className="padding--sm margin--none" | {props.label} |
| `Fragment` | fragment | *none* | <ASTViewer> |
| `SimpleField` | component | label="typeToString()", value={props.string} | *none* |
| `ASTViewer` | component | onHoverNode={props.onHoverNode}, value={props.type} | *none* |
| `div` | element | className={astStyles.list} | text: "None" |
| `div` | element | *none* | text: "TypeChecker not available" |
| `div` | element | *none* | *none* |
| `Fragment` | fragment | *none* | <h4>, <ASTViewer>, <TypeGroup>, <TypeGroup>, <TypeGroup>, <TypeGroup>, <TypeGroup> |
| `h4` | element | className="padding--sm margin--none" | text: "Node" |
| `ASTViewer` | component | onHoverNode={onHoverNode}, value={value} | *none* |
| `TypeGroup` | component | label="Type", onHoverNode={onHoverNode}, string={computed.typeString}, type={computed.type} | *none* |
| `TypeGroup` | component | label="Contextual Type", onHoverNode={onHoverNode}, string={computed.contextualTypeString}, type={computed.contextualType} | *none* |
| `TypeGroup` | component | label="Symbol", onHoverNode={onHoverNode}, type={computed.symbol} | *none* |
| `TypeGroup` | component | label="Signature", onHoverNode={onHoverNode}, type={computed.signature} | *none* |
| `TypeGroup` | component | label="FlowNode", onHoverNode={onHoverNode}, type={computed.flowNode} | *none* |


---

## Functions

### `SimpleField(props: SimpleFieldProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function SimpleField(props: SimpleFieldProps): React.JSX.Element {
  return (
    <div className={astStyles.list}>
      <span className={astStyles.propClass}>{props.label}</span>
      <span>: </span>
      <span className={astStyles.propString}>{String(props.value)}</span>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `props: SimpleFieldProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `String`
### `TypeGroup(props: TypeGroupProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function TypeGroup(props: TypeGroupProps): React.JSX.Element {
  return (
    <>
      <h4 className="padding--sm margin--none">{props.label}</h4>
      {props.type ? (
        <>
          {props.string && (
            <SimpleField label="typeToString()" value={props.string} />
          )}
          <ASTViewer onHoverNode={props.onHoverNode} value={props.type} />
        </>
      ) : (
        <div className={astStyles.list}>None</div>
      )}
    </>
  );
}
```
</details>

- **Parameters**:
  - `props: TypeGroupProps`
- **Return Type**: `React.JSX.Element`
### `TypeInfo({
  onHoverNode,
  typeChecker,
  value,
}: TypeInfoProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function TypeInfo({
  onHoverNode,
  typeChecker,
  value,
}: TypeInfoProps): React.JSX.Element {
  const computed = useMemo(() => {
    if (!typeChecker) {
      return undefined;
    }
    const info: InfoModel = {};
    try {
      const type = typeChecker.getTypeAtLocation(value);
      info.type = type;
      info.typeString = typeChecker.typeToString(type);
      info.symbol = type.getSymbol();
      let signature = type.getCallSignatures();
      if (signature.length === 0) {
        signature = type.getConstructSignatures();
      }
      info.signature = signature.length > 0 ? signature : undefined;
      // @ts-expect-error not part of public api
      info.flowNode = value.flowNode ?? value.endFlowNode ?? undefined;
    } catch (e: unknown) {
      info.type = e;
    }
    try {
      // @ts-expect-error just fail if a node type is not correct
      const contextualType = typeChecker.getContextualType(value);
      info.contextualType = contextualType;
      if (contextualType) {
        info.contextualTypeString = typeChecker.typeToString(contextualType);
      }
    } catch {
      info.contextualType = undefined;
    }
    return info;
  }, [value, typeChecker]);

  if (!typeChecker || !computed) {
    return <div>TypeChecker not available</div>;
  }

  return (
    <div>
      <>
        <h4 className="padding--sm margin--none">Node</h4>
        <ASTViewer onHoverNode={onHoverNode} value={value} />
        <TypeGroup
          label="Type"
          onHoverNode={onHoverNode}
          string={computed.typeString}
          type={computed.type}
        />
        <TypeGroup
          label="Contextual Type"
          onHoverNode={onHoverNode}
          string={computed.contextualTypeString}
          type={computed.contextualType}
        />
        <TypeGroup
          label="Symbol"
          onHoverNode={onHoverNode}
          type={computed.symbol}
        />
        <TypeGroup
          label="Signature"
          onHoverNode={onHoverNode}
          type={computed.signature}
        />
        <TypeGroup
          label="FlowNode"
          onHoverNode={onHoverNode}
          type={computed.flowNode}
        />
      </>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  onHoverNode,
  typeChecker,
  value,
}: TypeInfoProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useMemo (from react)`
  - `typeChecker.getTypeAtLocation`
  - `typeChecker.typeToString`
  - `type.getSymbol`
  - `type.getCallSignatures`
  - `type.getConstructSignatures`
  - `typeChecker.getContextualType`
- **Internal Comments**:
```
// @ts-expect-error not part of public api (x4)
// @ts-expect-error just fail if a node type is not correct (x2)
```


---

## Interfaces

### `TypeInfoProps`

<details><summary>Interface Code</summary>

```ts
export interface TypeInfoProps {
  readonly onHoverNode?: OnHoverNodeFn;
  readonly typeChecker?: ts.TypeChecker;
  readonly value: ts.Node;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `onHoverNode` | `OnHoverNodeFn` | ✓ |  |
| `typeChecker` | `ts.TypeChecker` | ✓ |  |
| `value` | `ts.Node` | ✗ |  |

### `InfoModel`

<details><summary>Interface Code</summary>

```ts
interface InfoModel {
  contextualType?: unknown;
  contextualTypeString?: string;
  flowNode?: unknown;
  signature?: unknown;
  symbol?: unknown;
  type?: unknown;
  typeString?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `contextualType` | `unknown` | ✓ |  |
| `contextualTypeString` | `string` | ✓ |  |
| `flowNode` | `unknown` | ✓ |  |
| `signature` | `unknown` | ✓ |  |
| `symbol` | `unknown` | ✓ |  |
| `type` | `unknown` | ✓ |  |
| `typeString` | `string` | ✓ |  |

### `SimpleFieldProps`

<details><summary>Interface Code</summary>

```ts
interface SimpleFieldProps {
  readonly label: string;
  readonly value: string | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `label` | `string` | ✗ |  |
| `value` | `string | undefined` | ✗ |  |

### `TypeGroupProps`

<details><summary>Interface Code</summary>

```ts
interface TypeGroupProps {
  readonly label: string;
  readonly onHoverNode?: OnHoverNodeFn;
  readonly string?: string;
  readonly type?: unknown;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `label` | `string` | ✗ |  |
| `onHoverNode` | `OnHoverNodeFn` | ✓ |  |
| `string` | `string` | ✓ |  |
| `type` | `unknown` | ✓ |  |


---