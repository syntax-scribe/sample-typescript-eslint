[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `HiddenItem.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---