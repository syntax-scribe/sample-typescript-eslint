[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `eslint.config.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
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

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/integration-tests/fixtures/flat-config-types-@types__eslint-v8/eslint.config.js`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatCompat` | `@eslint/eslintrc` |
| `eslint` | `@eslint/js` |
| `stylisticPlugin` | `@stylistic/eslint-plugin` |
| `vitestPlugin` | `@vitest/eslint-plugin` |
| `deprecationPlugin` | `eslint-plugin-deprecation` |
| `tseslint` | `typescript-eslint` |
| `__dirname` | `./dirname.cjs` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `compat` | `any` | let/var | `new FlatCompat({
  baseDirectory: __dirname,
  recommendedConfig: {},
  allConfig: {},
})` | ✗ |


---

## Functions

### `_otherCases(): void`

<details><summary>Code</summary>

```ts
function _otherCases() {
  // these are just tests for the types and are not seen by eslint so they can be whatever
  tseslint.config({
    plugins: {
      ['@stylistic']: stylisticPlugin,
      ['@typescript-eslint']: tseslint.plugin,
      ['deprecation']: deprecationPlugin,
      ['vitest']: vitestPlugin,
    },
  });
  tseslint.config(
    eslint.configs.recommended,
    ...tseslint.configs.recommended,
    stylisticPlugin.configs['recommended-flat'],
    vitestPlugin.configs.recommended,
  );
  tseslint.config(
    // @ts-expect-error
    compat.config(deprecationPlugin.configs.recommended),
    vitestPlugin.configs.recommended,
  );
  tseslint.config(
    // @ts-expect-error
    deprecationPlugin.configs.recommended,
    vitestPlugin.configs.recommended,
  );
}
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `tseslint.config`
  - `compat.config`
- **Internal Comments**:
```
// these are just tests for the types and are not seen by eslint so they can be whatever (x4)
// @ts-expect-error (x6)
```


---