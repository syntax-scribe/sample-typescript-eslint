[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PropertyValue.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 3 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/components/ast/PropertyValue.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `useMemo` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `styles` | `./ASTViewer.module.css` |
| `objType` | `./utils` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `span` | element | className={model.className} | {!expand ? `${model.shortValue}...` : model.value}, {' '}, <Link> |
| `Link` | component | className={styles.propEllipsis}, href="#read-more", onClick={(e): void => {
            e.preventDefault();
            setExpand(expand => !expand);
          }} | {!expand ? '(read more)' : '(read less)'} |
| `span` | element | className={model.className} | {model.value} |


---

## Functions

### `getSimpleModel(data: unknown): SimpleModel`

<details><summary>Code</summary>

```ts
function getSimpleModel(data: unknown): SimpleModel {
  if (typeof data === 'string') {
    const value = JSON.stringify(data);
    return {
      className: styles.propString,
      shortValue: value.length > 250 ? value.substring(0, 200) : undefined,
      value,
    };
  }
  if (typeof data === 'number') {
    return {
      className: styles.propNumber,
      value: String(data),
    };
  }
  if (typeof data === 'bigint') {
    return {
      className: styles.propNumber,
      value: `${data}n`,
    };
  }
  if (data instanceof RegExp) {
    return {
      className: styles.propRegExp,
      value: String(data),
    };
  }
  if (data == null) {
    return {
      className: styles.propEmpty,
      value: String(data),
    };
  }
  if (typeof data === 'boolean') {
    return {
      className: styles.propBoolean,
      value: data ? 'true' : 'false',
    };
  }
  if (data instanceof Error) {
    return {
      className: styles.propError,
      value: `Error: ${data.message}`,
    };
  }
  return {
    className: styles.propClass,
    value: objType(data),
  };
}
```
</details>

- **Parameters**:
  - `data: unknown`
- **Return Type**: `SimpleModel`
- **Calls**:
  - `JSON.stringify`
  - `value.substring`
  - `String`
  - `objType (from ./utils)`
### `PropertyValue({ value }: PropertyValueProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function PropertyValue({ value }: PropertyValueProps): React.JSX.Element {
  const [expand, setExpand] = useState(false);

  const model = useMemo(() => getSimpleModel(value), [value]);

  if (model.shortValue) {
    return (
      <span className={model.className}>
        {!expand ? `${model.shortValue}...` : model.value}{' '}
        <Link
          className={styles.propEllipsis}
          href="#read-more"
          onClick={(e): void => {
            e.preventDefault();
            setExpand(expand => !expand);
          }}
        >
          {!expand ? '(read more)' : '(read less)'}
        </Link>
      </span>
    );
  }

  return <span className={model.className}>{model.value}</span>;
}
```
</details>

- **Parameters**:
  - `{ value }: PropertyValueProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useMemo (from react)`
  - `getSimpleModel`
  - `e.preventDefault`
  - `setExpand`

---

## Interfaces

### `PropertyValueProps`

<details><summary>Interface Code</summary>

```ts
export interface PropertyValueProps {
  readonly value: unknown;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `value` | `unknown` | ✗ |  |

### `SimpleModel`

<details><summary>Interface Code</summary>

```ts
interface SimpleModel {
  readonly className: string;
  readonly shortValue?: string;
  readonly value: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✗ |  |
| `shortValue` | `string` | ✓ |  |
| `value` | `string` | ✗ |  |


---