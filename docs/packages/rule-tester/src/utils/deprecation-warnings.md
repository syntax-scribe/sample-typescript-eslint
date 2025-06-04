[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deprecation-warnings.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/deprecation-warnings.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `deprecationWarningMessages` | `{ readonly ESLINT_LEGACY_ECMAFEATURES: "The 'ecmaFeatures' config file property is deprecated and has no effect."; }` | const | `{
  ESLINT_LEGACY_ECMAFEATURES:
    "The 'ecmaFeatures' config file property is deprecated and has no effect.",
} as const` | ✗ |
| `sourceFileErrorCache` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `message` | `"The 'ecmaFeatures' config file property is deprecated and has no effect."` | const | `deprecationWarningMessages[errorCode]` | ✗ |


---

## Functions

### `emitDeprecationWarning(source: string, errorCode: keyof typeof deprecationWarningMessages): void`

<details><summary>Code</summary>

```ts
export function emitDeprecationWarning(
  source: string,
  errorCode: keyof typeof deprecationWarningMessages,
): void {
  const cacheKey = JSON.stringify({ errorCode, source });

  if (sourceFileErrorCache.has(cacheKey)) {
    return;
  }

  sourceFileErrorCache.add(cacheKey);

  const rel = path.relative(process.cwd(), source);
  const message = deprecationWarningMessages[errorCode];

  process.emitWarning(
    `${message} (found in "${rel}")`,
    'DeprecationWarning',
    errorCode,
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Emits a deprecation warning containing a given filepath. A new deprecation warning is emitted
 * for each unique file path, but repeated invocations with the same file path have no effect.
 * No warnings are emitted if the `--no-deprecation` or `--no-warnings` Node runtime flags are active.
 * @param source The name of the configuration source to report the warning for.
 * @param errorCode The warning message to show.
 */
```

- **Parameters**:
  - `source: string`
  - `errorCode: keyof typeof deprecationWarningMessages`
- **Return Type**: `void`
- **Calls**:
  - `JSON.stringify`
  - `sourceFileErrorCache.has`
  - `sourceFileErrorCache.add`
  - `path.relative`
  - `process.cwd`
  - `process.emitWarning`

---