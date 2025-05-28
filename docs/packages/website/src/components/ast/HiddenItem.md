[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `HiddenItem.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 5 |
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
📂 **`packages/website/src/components/ast/HiddenItem.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useEffect` | `react` |
| `useState` | `react` |
| `React` | `react` |
| `styles` | `./ASTViewer.module.css` |
| `PropertyValue` | `./PropertyValue` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `span` | element | className={styles.hidden} | {isArray && !isComplex ? (
        value.map(([, item], index) => (
          <span key={`${level}_[${index}]`}>
            {index > 0 && ', '}
            <PropertyValue value={item} />
          </span>
        ))
      ) : isArray ? (
        <>
          {length} {length === 1 ? 'element' : 'elements'}
        </>
      ) : (
        value.map(([key], index) => (
          <span key={`${level}_[${index}]`}>
            {index > 0 && ', '}
            {key}
          </span>
        ))
      )} |
| `span` | element | key={`${level}_[${index}]`} | {index > 0 && ', '}, <PropertyValue> |
| `PropertyValue` | component | value={item} | *none* |
| `Fragment` | fragment | *none* | *none* |
| `span` | element | key={`${level}_[${index}]`} | {index > 0 && ', '}, {key} |


---

## Functions

### `HiddenItem({
  isArray,
  level,
  value,
}: HiddenItemProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function HiddenItem({
  isArray,
  level,
  value,
}: HiddenItemProps): React.JSX.Element {
  const [isComplex, setIsComplex] = useState<boolean>(true);
  const [length, setLength] = useState<number>(0);

  useEffect(() => {
    if (isArray) {
      const filtered = value.filter(([key]) => !isNaN(Number(key)));
      setIsComplex(filtered.some(([, item]) => typeof item !== 'number'));
      setLength(filtered.length);
    }
  }, [value, isArray]);

  return (
    <span className={styles.hidden}>
      {isArray && !isComplex ? (
        value.map(([, item], index) => (
          <span key={`${level}_[${index}]`}>
            {index > 0 && ', '}
            <PropertyValue value={item} />
          </span>
        ))
      ) : isArray ? (
        <>
          {length} {length === 1 ? 'element' : 'elements'}
        </>
      ) : (
        value.map(([key], index) => (
          <span key={`${level}_[${index}]`}>
            {index > 0 && ', '}
            {key}
          </span>
        ))
      )}
    </span>
  );
}
```
</details>

- **Parameters**:
  - `{
  isArray,
  level,
  value,
}: HiddenItemProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useState (from react)`
  - `useEffect (from react)`
  - `value.filter`
  - `isNaN`
  - `Number`
  - `setIsComplex`
  - `filtered.some`
  - `setLength`
  - `value.map`

---

## Interfaces

### `HiddenItemProps`

<details><summary>Interface Code</summary>

```ts
export interface HiddenItemProps {
  readonly isArray?: boolean;
  readonly level: string;
  readonly value: [string, unknown][];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `isArray` | `boolean` | ✓ |  |
| `level` | `string` | ✗ |  |
| `value` | `[string, unknown][]` | ✗ |  |


---