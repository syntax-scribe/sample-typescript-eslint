[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `SourceCodeFixer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 11 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/SourceCodeFixer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `hasOwnProperty` | `./hasOwnProperty` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `BOM` | `"﻿"` | const | `'\uFEFF'` | ✗ |
| `remainingMessages` | `LintMessage[]` | const | `[]` | ✗ |
| `fixes` | `LintMessageWithFix[]` | const | `[]` | ✗ |
| `bom` | `"" | "﻿"` | const | `sourceText.startsWith(BOM) ? BOM : ''` | ✗ |
| `text` | `string` | const | `bom ? sourceText.slice(1) : sourceText` | ✗ |
| `lastPos` | `number` | let/var | `Number.NEGATIVE_INFINITY` | ✗ |
| `output` | `string` | let/var | `bom` | ✗ |
| `fix` | `any` | const | `problem.fix` | ✗ |
| `start` | `any` | const | `fix.range[0]` | ✗ |
| `end` | `any` | const | `fix.range[1]` | ✗ |
| `fixesWereApplied` | `boolean` | let/var | `false` | ✗ |


---

## Functions

### `compareMessagesByFixRange(a: LintMessageWithFix, b: LintMessageWithFix): number`

<details><summary>Code</summary>

```ts
function compareMessagesByFixRange(
  a: LintMessageWithFix,
  b: LintMessageWithFix,
): number {
  return a.fix.range[0] - b.fix.range[0] || a.fix.range[1] - b.fix.range[1];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Compares items in a messages array by range.
 * @returns -1 if a comes before b, 1 if a comes after b, 0 if equal.
 */
```

- **Parameters**:
  - `a: LintMessageWithFix`
  - `b: LintMessageWithFix`
- **Return Type**: `number`
### `compareMessagesByLocation(a: LintMessage, b: LintMessage): number`

<details><summary>Code</summary>

```ts
function compareMessagesByLocation(a: LintMessage, b: LintMessage): number {
  // @ts-expect-error -- it's not possible for suggestions to reach this location
  return a.line - b.line || a.column - b.column;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Compares items in a messages array by line and column.
 * @returns -1 if a comes before b, 1 if a comes after b, 0 if equal.
 */
```

- **Parameters**:
  - `a: LintMessage`
  - `b: LintMessage`
- **Return Type**: `number`
- **Internal Comments**:
```
// @ts-expect-error -- it's not possible for suggestions to reach this location
```

### `applyFixes(sourceText: string, messages: readonly LintMessage[]): AppliedFixes`

<details><summary>Code</summary>

```ts
export function applyFixes(
  sourceText: string,
  messages: readonly LintMessage[],
): AppliedFixes {
  // clone the array
  const remainingMessages: LintMessage[] = [];
  const fixes: LintMessageWithFix[] = [];
  const bom = sourceText.startsWith(BOM) ? BOM : '';
  const text = bom ? sourceText.slice(1) : sourceText;
  let lastPos = Number.NEGATIVE_INFINITY;
  let output = bom;

  /**
   * Try to use the 'fix' from a problem.
   * @param problem The message object to apply fixes from
   * @returns Whether fix was successfully applied
   */
  function attemptFix(problem: LintMessageWithFix): boolean {
    const fix = problem.fix;
    const start = fix.range[0];
    const end = fix.range[1];

    // Remain it as a problem if it's overlapped or it's a negative range
    if (lastPos >= start || start > end) {
      remainingMessages.push(problem);
      return false;
    }

    // Remove BOM.
    if ((start < 0 && end >= 0) || (start === 0 && fix.text.startsWith(BOM))) {
      output = '';
    }

    // Make output to this fix.
    output += text.slice(Math.max(0, lastPos), Math.max(0, start));
    output += fix.text;
    lastPos = end;
    return true;
  }

  messages.forEach(problem => {
    if (hasOwnProperty(problem, 'fix')) {
      fixes.push(problem);
    } else {
      remainingMessages.push(problem);
    }
  });

  if (fixes.length) {
    let fixesWereApplied = false;

    for (const problem of fixes.sort(compareMessagesByFixRange)) {
      attemptFix(problem);

      /*
       * The only time attemptFix will fail is if a previous fix was
       * applied which conflicts with it.  So we can mark this as true.
       */
      fixesWereApplied = true;
    }
    output += text.slice(Math.max(0, lastPos));

    return {
      fixed: fixesWereApplied,
      messages: remainingMessages.sort(compareMessagesByLocation),
      output,
    };
  }

  return {
    fixed: false,
    messages,
    output: bom + text,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Applies the fixes specified by the messages to the given text. Tries to be
 * smart about the fixes and won't apply fixes over the same area in the text.
 * @param sourceText The text to apply the changes to.
 * @param  messages The array of messages reported by ESLint.
 * @returns An object containing the fixed text and any unfixed messages.
 */
```

- **Parameters**:
  - `sourceText: string`
  - `messages: readonly LintMessage[]`
- **Return Type**: `AppliedFixes`
- **Calls**:
  - `sourceText.startsWith`
  - `sourceText.slice`
  - `remainingMessages.push`
  - `fix.text.startsWith`
  - `text.slice`
  - `Math.max`
  - `messages.forEach`
  - `hasOwnProperty (from ./hasOwnProperty)`
  - `fixes.push`
  - `fixes.sort`
  - `attemptFix`
  - `remainingMessages.sort`
- **Internal Comments**:
```
// clone the array (x2)
/**
   * Try to use the 'fix' from a problem.
   * @param problem The message object to apply fixes from
   * @returns Whether fix was successfully applied
   */
// Remain it as a problem if it's overlapped or it's a negative range
// Remove BOM.
// Make output to this fix. (x3)
/*
       * The only time attemptFix will fail is if a previous fix was
       * applied which conflicts with it.  So we can mark this as true.
       */ (x3)
```

### `attemptFix(problem: LintMessageWithFix): boolean`

<details><summary>Code</summary>

```ts
function attemptFix(problem: LintMessageWithFix): boolean {
    const fix = problem.fix;
    const start = fix.range[0];
    const end = fix.range[1];

    // Remain it as a problem if it's overlapped or it's a negative range
    if (lastPos >= start || start > end) {
      remainingMessages.push(problem);
      return false;
    }

    // Remove BOM.
    if ((start < 0 && end >= 0) || (start === 0 && fix.text.startsWith(BOM))) {
      output = '';
    }

    // Make output to this fix.
    output += text.slice(Math.max(0, lastPos), Math.max(0, start));
    output += fix.text;
    lastPos = end;
    return true;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Try to use the 'fix' from a problem.
   * @param problem The message object to apply fixes from
   * @returns Whether fix was successfully applied
   */
```

- **Parameters**:
  - `problem: LintMessageWithFix`
- **Return Type**: `boolean`
- **Calls**:
  - `remainingMessages.push`
  - `fix.text.startsWith`
  - `text.slice`
  - `Math.max`
- **Internal Comments**:
```
// Remain it as a problem if it's overlapped or it's a negative range
// Remove BOM.
// Make output to this fix. (x3)
```


---

## Interfaces

### `AppliedFixes`

<details><summary>Interface Code</summary>

```ts
export interface AppliedFixes {
  fixed: boolean;
  messages: readonly LintMessage[];
  output: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fixed` | `boolean` | ✗ |  |
| `messages` | `readonly LintMessage[]` | ✗ |  |
| `output` | `string` | ✗ |  |


---

## Type Aliases

### `LintMessage`

```ts
type LintMessage = Linter.LintMessage | Linter.LintSuggestion;
```

### `LintMessageWithFix`

```ts
type LintMessageWithFix = LintMessage & Required<Pick<LintMessage, 'fix'>>;
```


---