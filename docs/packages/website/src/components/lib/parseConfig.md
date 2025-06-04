[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `parseConfig.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/parseConfig.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `EslintRC` | `../types` |
| `TSConfig` | `../types` |
| `isRecord` | `../ast/utils` |
| `ensureObject` | `./json` |
| `parseJSONObject` | `./json` |
| `toJson` | `./json` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `moduleRegexp` | `RegExp` | const | `/(module\.exports\s*=)/g` | ✗ |


---

## Functions

### `parseESLintRC(code: string): EslintRC`

<details><summary>Code</summary>

```ts
export function parseESLintRC(code?: string): EslintRC {
  if (code) {
    try {
      const parsed = parseJSONObject(code);
      parsed.rules = ensureObject(parsed.rules);

      if ('extends' in parsed) {
        parsed.extends =
          Array.isArray(parsed.extends) || typeof parsed.extends === 'string'
            ? parsed.extends
            : [];
      }
      return parsed as EslintRC;
    } catch (e) {
      console.error(e);
    }
  }
  return { rules: {} };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parse a .eslintrc string into an object.
 * This function is pretty naive, as it only validates rules and extends.
 */
```

- **Parameters**:
  - `code: string`
- **Return Type**: `EslintRC`
- **Calls**:
  - `parseJSONObject (from ./json)`
  - `ensureObject (from ./json)`
  - `Array.isArray`
  - `console.error`
### `parseTSConfig(code: string): TSConfig`

<details><summary>Code</summary>

```ts
export function parseTSConfig(code?: string): TSConfig {
  if (code) {
    try {
      const parsed = window.ts.parseConfigFileTextToJson(
        '/tsconfig.json',
        code,
      );
      if (parsed.error) {
        console.error(parsed.error);
      }
      if (isRecord(parsed.config)) {
        return parsed.config as TSConfig;
      }
    } catch (e) {
      console.error(e);
    }
  }
  return { compilerOptions: {} };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parse a tsconfig.json string into an object.
 * This is done by typescript compiler.
 */
```

- **Parameters**:
  - `code: string`
- **Return Type**: `TSConfig`
- **Calls**:
  - `window.ts.parseConfigFileTextToJson`
  - `console.error`
  - `isRecord (from ../ast/utils)`
### `constrainedScopeEval(obj: string): unknown`

<details><summary>Code</summary>

```ts
function constrainedScopeEval(obj: string): unknown {
  // eslint-disable-next-line @typescript-eslint/no-implied-eval, @typescript-eslint/no-unsafe-call
  return new Function(`
    "use strict";
    var module = { exports: {} };
    (${obj});
    return module.exports
  `)();
}
```
</details>

- **Parameters**:
  - `obj: string`
- **Return Type**: `unknown`
- **Calls**:
  - `complex_call_1505`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-implied-eval, @typescript-eslint/no-unsafe-call
```

### `tryParseEslintModule(value: string): string`

<details><summary>Code</summary>

```ts
export function tryParseEslintModule(value: string): string {
  try {
    if (moduleRegexp.test(value)) {
      const newValue = toJson(constrainedScopeEval(value));
      if (newValue !== value) {
        return newValue;
      }
    }
  } catch (e) {
    console.error(e);
  }
  return value;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Evaluate a string that contains a module.exports assignment.
 */
```

- **Parameters**:
  - `value: string`
- **Return Type**: `string`
- **Calls**:
  - `moduleRegexp.test`
  - `toJson (from ./json)`
  - `constrainedScopeEval`
  - `console.error`

---