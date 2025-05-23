[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `scroll-into.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/scroll-into.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---