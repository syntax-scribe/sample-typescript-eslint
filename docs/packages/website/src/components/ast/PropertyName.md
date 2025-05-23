[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PropertyName.tsx`

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
📂 **`packages/website/src/components/ast/PropertyName.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `KeyboardEvent` | `react` |
| `MouseEvent` | `react` |
| `Link` | `@docusaurus/Link` |
| `useCallback` | `react` |
| `React` | `react` |


---

## Functions

### `PropertyName({
  className,
  onClick: onClickProp,
  onHover: onHoverProp,
  value,
}: PropertyNameProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function PropertyName({
  className,
  onClick: onClickProp,
  onHover: onHoverProp,
  value,
}: PropertyNameProps): React.JSX.Element {
  const onClick = useCallback(
    (e: MouseEvent<HTMLElement>) => {
      e.preventDefault();
      onClickProp?.();
    },
    [onClickProp],
  );

  const onMouseEnter = useCallback(() => {
    onHoverProp?.(true);
  }, [onHoverProp]);

  const onMouseLeave = useCallback(() => {
    onHoverProp?.(false);
  }, [onHoverProp]);

  const onKeyDown = useCallback(
    (e: KeyboardEvent<HTMLElement>) => {
      if (e.code === 'Space') {
        e.preventDefault();
        onClickProp?.();
      }
    },
    [onClickProp],
  );

  return (
    <Link
      className={className}
      href={`#${value}`}
      onClick={onClick}
      onKeyDown={onKeyDown}
      onMouseEnter={onMouseEnter}
      onMouseLeave={onMouseLeave}
      role="button"
      tabIndex={onClickProp && 0}
    >
      {value}
    </Link>
  );
}
```
</details>

- **Parameters**:
  - `{
  className,
  onClick: onClickProp,
  onHover: onHoverProp,
  value,
}: PropertyNameProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useCallback (from react)`
  - `e.preventDefault`
  - `onClickProp`
  - `onHoverProp`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `PropertyNameProps`

<details><summary>Interface Code</summary>

```ts
export interface PropertyNameProps {
  readonly className?: string;
  readonly onClick?: () => void;
  readonly onHover?: (e: boolean) => void;
  readonly value?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `onClick` | `() => void` | ✓ |  |
| `onHover` | `(e: boolean) => void` | ✓ |  |
| `value` | `string` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---