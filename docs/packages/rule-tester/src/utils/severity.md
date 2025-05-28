[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `severity.ts`

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
📂 **`packages/rule-tester/src/utils/severity.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SharedConfig` | `@typescript-eslint/utils/ts-eslint` |


---

## Functions

### `normalizeSeverityToString(severity: SharedConfig.RuleLevel): SharedConfig.SeverityString`

<details><summary>Code</summary>

```ts
export function normalizeSeverityToString(
  severity: SharedConfig.RuleLevel,
): SharedConfig.SeverityString {
  if ([2, '2', 'error'].includes(severity)) {
    return 'error';
  }
  if ([1, '1', 'warn'].includes(severity)) {
    return 'warn';
  }
  if ([0, '0', 'off'].includes(severity)) {
    return 'off';
  }
  throw new Error(`Invalid severity value: ${severity}`);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert severity value of different types to a string.
 * @param  severity severity value
 * @throws error if severity is invalid
 */
```

- **Parameters**:
  - `severity: SharedConfig.RuleLevel`
- **Return Type**: `SharedConfig.SeverityString`
- **Calls**:
  - `[2, '2', 'error'].includes`
  - `[1, '1', 'warn'].includes`
  - `[0, '0', 'off'].includes`
### `normalizeSeverityToNumber(severity: SharedConfig.RuleLevel): SharedConfig.Severity`

<details><summary>Code</summary>

```ts
export function normalizeSeverityToNumber(
  severity: SharedConfig.RuleLevel,
): SharedConfig.Severity {
  if ([2, '2', 'error'].includes(severity)) {
    return 2;
  }
  if ([1, '1', 'warn'].includes(severity)) {
    return 1;
  }
  if ([0, '0', 'off'].includes(severity)) {
    return 0;
  }
  throw new Error(`Invalid severity value: ${severity}`);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Convert severity value of different types to a number.
 * @param  severity severity value
 * @throws error if severity is invalid
 */
```

- **Parameters**:
  - `severity: SharedConfig.RuleLevel`
- **Return Type**: `SharedConfig.Severity`
- **Calls**:
  - `[2, '2', 'error'].includes`
  - `[1, '1', 'warn'].includes`
  - `[0, '0', 'off'].includes`

---