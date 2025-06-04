[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `scroll-into.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/scroll-into.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `isBelow` | `boolean` | const | `rect.top < 0` | ✗ |
| `isAbove` | `boolean` | const | `rect.bottom > window.innerHeight` | ✗ |


---

## Functions

### `scrollIntoViewIfNeeded(target: Element): void`

<details><summary>Code</summary>

```ts
export function scrollIntoViewIfNeeded(target: Element): void {
  const rect = target.getBoundingClientRect();
  const isBelow = rect.top < 0;
  const isAbove = rect.bottom > window.innerHeight;
  if ((isAbove && isBelow) || rect.height > window.innerHeight) {
    target.scrollIntoView({
      behavior: 'smooth',
      block: 'start',
      inline: 'start',
    });
    return;
  }
  // Target is outside the viewport from the bottom
  if (isAbove) {
    target.scrollIntoView({
      behavior: 'smooth',
      block: 'center',
      inline: 'center',
    });
    return;
  }
  // Target is outside the view from the top
  if (isBelow) {
    target.scrollIntoView({
      behavior: 'smooth',
      block: 'center',
      inline: 'center',
    });
    return;
  }
}
```
</details>

- **JSDoc**:
```ts
/**
 * Scroll the target element into view if it is not already visible.
 */
```

- **Parameters**:
  - `target: Element`
- **Return Type**: `void`
- **Calls**:
  - `target.getBoundingClientRect`
  - `target.scrollIntoView`
- **Internal Comments**:
```
// Target is outside the viewport from the bottom
// Target is outside the view from the top
```


---