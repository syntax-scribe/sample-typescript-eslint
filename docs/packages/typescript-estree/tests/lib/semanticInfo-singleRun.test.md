[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `semanticInfo-singleRun.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/typescript-estree/tests/lib/semanticInfo-singleRun.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `createProgramFromConfigFileOriginal` | `../../src/create-program/useProvidedPrograms` |
| `clearParseAndGenerateServicesCalls` | `../../src/parser` |
| `clearProgramCache` | `../../src/parser` |
| `parseAndGenerateServices` | `../../src/parser` |


---

## Functions

### `resolvedProject(p: string): string`

<details><summary>Code</summary>

```ts
(p: string): string => path.resolve(FIXTURES_DIR, p)
```
</details>

- **Parameters**:
  - `p: string`
- **Return Type**: `string`
- **Calls**:
  - `path.resolve`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `MockProgramWithConfigFile`

<details><summary>Interface Code</summary>

```ts
interface MockProgramWithConfigFile {
  __FROM_CONFIG_FILE__?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `__FROM_CONFIG_FILE__` | `string` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---