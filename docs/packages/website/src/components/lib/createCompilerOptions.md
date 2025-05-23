[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `createCompilerOptions.ts`

## 📚 Table of Contents

- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/lib/createCompilerOptions.ts`**

## 📦 Imports

> No imports found in this file.


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---