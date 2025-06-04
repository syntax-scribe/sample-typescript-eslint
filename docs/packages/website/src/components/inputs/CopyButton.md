[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `CopyButton.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 1 |
| 💠 JSX Elements | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `cache` | `Set<unknown>` | const | `new Set()` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.copyButtonContainer} | <Tooltip> |
| `Tooltip` | component | open={on}, text="Copied" | <button> |
| `button` | element | aria-label={!on ? 'Copy code to clipboard' : 'Copied'}, className={clsx(styles.copyButton, className, 'button')}, disabled={on}, onClick={onCopy} | <CopyIcon>, <CheckIcon> |
| `CopyIcon` | component | className={styles.copyIcon}, height="18", width="18" | *none* |
| `CheckIcon` | component | className={styles.checkIcon}, height="18", width="18" | *none* |


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