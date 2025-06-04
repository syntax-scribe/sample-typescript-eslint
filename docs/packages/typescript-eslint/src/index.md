[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |
| 🔄 Re-exports | 1 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Re-exports](#re-exports)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-eslint/src/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `pluginBase` | `@typescript-eslint/eslint-plugin` |
| `rawPlugin` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/raw-plugin` |
| `config` | `./config-helper` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parser` | `TSESLint.FlatConfig.Parser` | const | `rawPlugin.parser` | ✓ |
| `plugin` | `TSESLint.FlatConfig.Plugin` | const | `pluginBase as Omit<
  typeof pluginBase,
  'configs'
>` | ✓ |
| `configs` | `{ all: any; base: any; disableTypeChecked: any; eslintRecommended: any; recommended: any; recommendedTypeChecked: any; recommendedTypeCheckedOnly: any; strict: any; strictTypeChecked: any; strictTypeCheckedOnly: any; stylistic: any; stylisticTypeChecked: any; stylisticTypeCheckedOnly: any; }` | const | `{
  /**
   * Enables each the rules provided as a part of typescript-eslint. Note that many rules are not applicable in all codebases, or are meant to be configured.
   * @see {@link https://typescript-eslint.io/users/configs#all}
   */
  all: rawPlugin.flatConfigs['flat/all'],

  /**
   * A minimal ruleset that sets only the required parser and plugin options needed to run typescript-eslint.
   * We don't recommend using this directly; instead, extend from an earlier recommended rule.
   * @see {@link https://typescript-eslint.io/users/configs#base}
   */
  base: rawPlugin.flatConfigs['flat/base'],

  /**
   * A utility ruleset that will disable type-aware linting and all type-aware rules available in our project.
   * @see {@link https://typescript-eslint.io/users/configs#disable-type-checked}
   */
  disableTypeChecked: rawPlugin.flatConfigs['flat/disable-type-checked'],

  /**
   * This is a compatibility ruleset that:
   * - disables rules from eslint:recommended which are already handled by TypeScript.
   * - enables rules that make sense due to TS's typechecking / transpilation.
   * @see {@link https://typescript-eslint.io/users/configs/#eslint-recommended}
   */
  eslintRecommended: rawPlugin.flatConfigs['flat/eslint-recommended'],

  /**
   * Recommended rules for code correctness that you can drop in without additional configuration.
   * @see {@link https://typescript-eslint.io/users/configs#recommended}
   */
  recommended: rawPlugin.flatConfigs['flat/recommended'],

  /**
   * Contains all of `recommended` along with additional recommended rules that require type information.
   * @see {@link https://typescript-eslint.io/users/configs#recommended-type-checked}
   */
  recommendedTypeChecked:
    rawPlugin.flatConfigs['flat/recommended-type-checked'],

  /**
   * A version of `recommended` that only contains type-checked rules and disables of any corresponding core ESLint rules.
   * @see {@link https://typescript-eslint.io/users/configs#recommended-type-checked-only}
   */
  recommendedTypeCheckedOnly:
    rawPlugin.flatConfigs['flat/recommended-type-checked-only'],

  /**
   * Contains all of `recommended`, as well as additional strict rules that can also catch bugs.
   * @see {@link https://typescript-eslint.io/users/configs#strict}
   */
  strict: rawPlugin.flatConfigs['flat/strict'],

  /**
   * Contains all of `recommended`, `recommended-type-checked`, and `strict`, along with additional strict rules that require type information.
   * @see {@link https://typescript-eslint.io/users/configs#strict-type-checked}
   */
  strictTypeChecked: rawPlugin.flatConfigs['flat/strict-type-checked'],

  /**
   * A version of `strict` that only contains type-checked rules and disables of any corresponding core ESLint rules.
   * @see {@link https://typescript-eslint.io/users/configs#strict-type-checked-only}
   */
  strictTypeCheckedOnly: rawPlugin.flatConfigs['flat/strict-type-checked-only'],

  /**
   * Rules considered to be best practice for modern TypeScript codebases, but that do not impact program logic.
   * @see {@link https://typescript-eslint.io/users/configs#stylistic}
   */
  stylistic: rawPlugin.flatConfigs['flat/stylistic'],

  /**
   * Contains all of `stylistic`, along with additional stylistic rules that require type information.
   * @see {@link https://typescript-eslint.io/users/configs#stylistic-type-checked}
   */
  stylisticTypeChecked: rawPlugin.flatConfigs['flat/stylistic-type-checked'],

  /**
   * A version of `stylistic` that only contains type-checked rules and disables of any corresponding core ESLint rules.
   * @see {@link https://typescript-eslint.io/users/configs#stylistic-type-checked-only}
   */
  stylisticTypeCheckedOnly:
    rawPlugin.flatConfigs['flat/stylistic-type-checked-only'],
}` | ✓ |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `./config-helper` | config, ConfigWithExtends, InfiniteDepthConfigWithExtends, ConfigArray |


---

## Type Aliases

### `Config`

```ts
type Config = TSESLint.FlatConfig.ConfigFile;
```


---