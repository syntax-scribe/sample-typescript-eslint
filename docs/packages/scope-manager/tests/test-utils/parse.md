[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parse.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/parse.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AnalyzeOptions` | `../../src/analyze` |
| `analyze` | `../../src/analyze` |


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

## Classes

> No classes found in this file.


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