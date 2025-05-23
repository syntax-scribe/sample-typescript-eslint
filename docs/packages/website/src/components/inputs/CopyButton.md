[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `CopyButton.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/inputs/CopyButton.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `CopyIcon` | `@theme/Icon/Copy` |
| `CheckIcon` | `@theme/Icon/Success` |
| `clsx` | `clsx` |
| `React` | `react` |
| `useClipboard` | `../../hooks/useClipboard` |
| `styles` | `./CopyButton.module.css` |
| `Tooltip` | `./Tooltip` |


---

## Functions

### `jsonStringifyRecursive(obj: unknown): string`

<details><summary>Code</summary>

```ts
function jsonStringifyRecursive(obj: unknown): string {
  const cache = new Set();
  return JSON.stringify(
    obj,
    (key, value: unknown) => {
      if (typeof value === 'object' && value != null) {
        if (cache.has(value)) {
          return;
        }
        cache.add(value);
      }
      return value;
    },
    2,
  );
}
```
</details>

- **Parameters**:
  - `obj: unknown`
- **Return Type**: `string`
- **Calls**:
  - `JSON.stringify`
  - `cache.has`
  - `cache.add`
### `CopyButton({ className, value }: CopyButtonProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
function CopyButton({ className, value }: CopyButtonProps): React.JSX.Element {
  const [on, onCopy] = useClipboard(() => jsonStringifyRecursive(value));

  return (
    <div className={styles.copyButtonContainer}>
      <Tooltip open={on} text="Copied">
        <button
          aria-label={!on ? 'Copy code to clipboard' : 'Copied'}
          className={clsx(styles.copyButton, className, 'button')}
          disabled={on}
          onClick={onCopy}
        >
          <CopyIcon className={styles.copyIcon} height="18" width="18" />
          <CheckIcon className={styles.checkIcon} height="18" width="18" />
        </button>
      </Tooltip>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{ className, value }: CopyButtonProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useClipboard (from ../../hooks/useClipboard)`
  - `jsonStringifyRecursive`
  - `clsx (from clsx)`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `CopyButtonProps`

<details><summary>Interface Code</summary>

```ts
export interface CopyButtonProps {
  readonly className?: string;
  readonly value: unknown;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✓ |  |
| `value` | `unknown` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---