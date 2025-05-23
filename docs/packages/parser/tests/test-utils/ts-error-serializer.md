[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ts-error-serializer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 6
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/test-utils/ts-error-serializer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SnapshotSerializer` | `vitest` |
| `TSError` | `@typescript-eslint/typescript-estree` |


---

## Functions

### `format(value: unknown): string`

<details><summary>Code</summary>

```ts
(value: unknown): string =>
      printer(value, config, indentation, depth + 1, refs)
```
</details>

- **Parameters**:
  - `value: unknown`
- **Return Type**: `string`
- **Calls**:
  - `printer`
### `test(val: unknown): val is TSError`

<details><summary>Code</summary>

```ts
(val: unknown): val is TSError => val instanceof TSError
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `val is TSError`
### `test(val: unknown): val is TSError`

<details><summary>Code</summary>

```ts
(val: unknown): val is TSError => val instanceof TSError
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `val is TSError`
### `test(val: unknown): val is TSError`

<details><summary>Code</summary>

```ts
(val: unknown): val is TSError => val instanceof TSError
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `val is TSError`
### `serialize(val: TSError, config: any, indentation: any, depth: any, refs: any, printer: any): string`

<details><summary>Code</summary>

```ts
serialize(val: TSError, config, indentation, depth, refs, printer) {
    const format = (value: unknown): string =>
      printer(value, config, indentation, depth + 1, refs);
    return (
      `${val.name} {\n` +
      `${config.indent}"column": ${format(val.column)},\n` +
      `${config.indent}"index": ${format(val.index)},\n` +
      `${config.indent}"lineNumber": ${format(val.lineNumber)},\n` +
      `${config.indent}"message": ${format(val.message)},\n` +
      `}`
    );
  }
```
</details>

- **Parameters**:
  - `val: TSError`
  - `config: any`
  - `indentation: any`
  - `depth: any`
  - `refs: any`
  - `printer: any`
- **Return Type**: `string`
- **Calls**:
  - `printer`
  - `format`
### `serializer.test(val: unknown): val is TSError`

<details><summary>Code</summary>

```ts
(val: unknown): val is TSError => val instanceof TSError
```
</details>

- **Parameters**:
  - `val: unknown`
- **Return Type**: `val is TSError`

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