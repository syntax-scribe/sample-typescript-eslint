[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `deprecation-warnings.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/deprecation-warnings.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---