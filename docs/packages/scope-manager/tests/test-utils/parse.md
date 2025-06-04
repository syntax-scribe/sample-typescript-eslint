[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parse.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 3 |
| 🔄 Re-exports | 1 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/parse.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AnalyzeOptions` | `../../src/analyze` |
| `analyze` | `../../src/analyze` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PARSER_OPTIONS` | `{ range: boolean; }` | const | `{
  // the analyser requires ranges to work
  range: true,
}` | ✗ |
| `DEFAULT_ANALYZE_OPTIONS` | `{ lib: any[]; }` | const | `{
  // include no libs so we don't pollute tests
  lib: [],
}` | ✗ |
| `analyzeOptions` | `any` | const | `{
    ...DEFAULT_ANALYZE_OPTIONS,
    ...(typeof sourceTypeOrAnalyzeOption === 'string'
      ? { sourceType: sourceTypeOrAnalyzeOption }
      : sourceTypeOrAnalyzeOption),
  }` | ✗ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `../../src/analyze` | AnalyzeOptions |


---

## Functions

### `parse(code: string, sourceTypeOrParserOptions: | SourceType
    | tseslint.TSESTreeOptions): ReturnType<typeof tseslint.parse>`

<details><summary>Code</summary>

```ts
export function parse(
  code: string,
  sourceTypeOrParserOptions:
    | SourceType
    | tseslint.TSESTreeOptions = DEFAULT_PARSER_OPTIONS,
): ReturnType<typeof tseslint.parse> {
  return tseslint.parse(code, {
    ...DEFAULT_PARSER_OPTIONS,
    ...(typeof sourceTypeOrParserOptions === 'string'
      ? {
          sourceType: sourceTypeOrParserOptions,
        }
      : sourceTypeOrParserOptions),
  });
}
```
</details>

- **Parameters**:
  - `code: string`
  - `sourceTypeOrParserOptions: | SourceType
    | tseslint.TSESTreeOptions`
- **Return Type**: `ReturnType<typeof tseslint.parse>`
- **Calls**:
  - `tseslint.parse`
### `parseAndAnalyze(code: string, sourceType: SourceType): ParseAndAnalyze`

<details><summary>Code</summary>

```ts
export function parseAndAnalyze(
  code: string,
  sourceType: SourceType,
): ParseAndAnalyze;
```
</details>

- **Parameters**:
  - `code: string`
  - `sourceType: SourceType`
- **Return Type**: `ParseAndAnalyze`

---

## Interfaces

### `ParseAndAnalyze`

<details><summary>Interface Code</summary>

```ts
export interface ParseAndAnalyze {
  ast: ReturnType<typeof tseslint.parse>;
  scopeManager: ReturnType<typeof analyze>;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `ast` | `ReturnType<typeof tseslint.parse>` | ✗ |  |
| `scopeManager` | `ReturnType<typeof analyze>` | ✗ |  |


---

## Type Aliases

### `SourceType`

```ts
type SourceType = AnalyzeOptions['sourceType'];
```


---