[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `eslint.config.js`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---