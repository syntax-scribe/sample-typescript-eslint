[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `interpolate.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/interpolate.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ReportDescriptorMessageData` | `@typescript-eslint/utils/ts-eslint` |


---

## Functions

### `getPlaceholderMatcher(): RegExp`

<details><summary>Code</summary>

```ts
export function getPlaceholderMatcher(): RegExp {
  return /\{\{([^{}]+)\}\}/gu;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns a global expression matching placeholders in messages.
 */
```

- **Return Type**: `RegExp`
### `interpolate(text: string, data: ReportDescriptorMessageData | undefined): string`

<details><summary>Code</summary>

```ts
export function interpolate(
  text: string,
  data: ReportDescriptorMessageData | undefined,
): string {
  if (!data) {
    return text;
  }

  const matcher = getPlaceholderMatcher();

  // Substitution content for any {{ }} markers.
  return text.replace(matcher, (fullMatch, termWithWhitespace: string) => {
    const term = termWithWhitespace.trim();

    if (term in data) {
      return String(data[term]);
    }

    // Preserve old behavior: If parameter name not provided, don't replace it.
    return fullMatch;
  });
}
```
</details>

- **Parameters**:
  - `text: string`
  - `data: ReportDescriptorMessageData | undefined`
- **Return Type**: `string`
- **Calls**:
  - `getPlaceholderMatcher`
  - `text.replace`
  - `termWithWhitespace.trim`
  - `String`
- **Internal Comments**:
```
// Substitution content for any {{ }} markers.
// Preserve old behavior: If parameter name not provided, don't replace it.
```


---