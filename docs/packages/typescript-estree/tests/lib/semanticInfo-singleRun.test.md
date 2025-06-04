[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `semanticInfo-singleRun.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 12 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

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

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `mockProgram` | `{ getCompilerOptions(): unknown; getSourceFile(): void; getTypeChecker(): void; }` | const | `{
  getCompilerOptions(): unknown {
    return {};
  },
  getSourceFile(): void {
    return;
  },
  getTypeChecker(): void {
    return;
  },
}` | ✗ |
| `actual` | `any` | let/var | `await importOriginal()` | ✗ |
| `actual` | `any` | let/var | `await importOriginal()` | ✗ |
| `actual` | `any` | let/var | `await importOriginal()` | ✗ |
| `code` | `"const foo = 5;"` | const | `'const foo = 5;'` | ✗ |
| `tsconfigs` | `string[]` | const | `['./non-matching-tsconfig.json', './tsconfig.json']` | ✗ |
| `options` | `{ readonly allowAutomaticSingleRunInference: true; readonly filePath: any; readonly loggerFn: false; readonly project: string[]; readonly tsconfigRootDir: string; }` | const | `{
  allowAutomaticSingleRunInference: true,
  filePath: testFiles[0],
  loggerFn: false,
  project: tsconfigs,
  tsconfigRootDir: FIXTURES_DIR,
} as const` | ✗ |
| `resultProgram` | `any` | const | `parseAndGenerateServices(code, options).services
        .program` | ✗ |
| `resultProgram` | `any` | const | `parseAndGenerateServices(code, options).services
        .program` | ✗ |
| `resultProgram` | `any` | const | `parseAndGenerateServices(code, options).services
        .program` | ✗ |
| `optionsWithReversedTsconfigs` | `{ project: string[]; allowAutomaticSingleRunInference: true; filePath: any; loggerFn: false; tsconfigRootDir: string; }` | const | `{
        ...options,
        //  Now the matching tsconfig comes first
        project: [...options.project].reverse(),
      }` | ✗ |
| `resultProgram` | `any` | const | `parseAndGenerateServices(
        code,
        optionsWithReversedTsconfigs,
      ).services.program` | ✗ |


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