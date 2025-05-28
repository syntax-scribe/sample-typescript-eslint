[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createCompilerOptions.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 0 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/createCompilerOptions.ts`**

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `options` | `any` | const | `config.options` | ✗ |


---

## Functions

### `createCompilerOptions(tsConfig: Record<string, unknown>): ts.CompilerOptions`

<details><summary>Code</summary>

```ts
export function createCompilerOptions(
  tsConfig: Record<string, unknown> = {},
): ts.CompilerOptions {
  const config = window.ts.convertCompilerOptionsFromJson(
    {
      jsx: 'preserve',
      module: 'esnext',
      target: 'esnext',
      ...tsConfig,
      allowJs: true,
      baseUrl: undefined,
      lib: Array.isArray(tsConfig.lib) ? tsConfig.lib : undefined,
      moduleDetection: undefined,
      moduleResolution: undefined,
      paths: undefined,
      plugins: undefined,
      typeRoots: undefined,
    },
    '/tsconfig.json',
  );

  const options = config.options;

  options.lib ??= [window.ts.getDefaultLibFileName(options)];

  return options;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Converts compiler options from JSON to ts.CompilerOptions
 */
```

- **Parameters**:
  - `tsConfig: Record<string, unknown>`
- **Return Type**: `ts.CompilerOptions`
- **Calls**:
  - `window.ts.convertCompilerOptionsFromJson`
  - `Array.isArray`
  - `window.ts.getDefaultLibFileName`

---