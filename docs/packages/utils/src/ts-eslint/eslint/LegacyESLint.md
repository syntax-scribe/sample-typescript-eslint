[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `LegacyESLint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 2 |
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 7 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/eslint/LegacyESLint.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintLegacyESLint` | `eslint/use-at-your-own-risk` |
| `ClassicConfig` | `../Config` |
| `Linter` | `../Linter` |


---

## Classes

### `LegacyESLintBase`

<details><summary>Class Code</summary>

```ts
declare class LegacyESLintBase extends Shared.ESLintBase<
  ClassicConfig.Config,
  LegacyESLint.ESLintOptions
> {
  static readonly configType: 'eslintrc';
}
```
</details>

### `LegacyESLint`

<details><summary>Class Code</summary>

```ts
export class LegacyESLint extends (ESLintLegacyESLint as typeof LegacyESLintBase) {}
```
</details>


---

## Interfaces

### `ESLintOptions`

<details><summary>Interface Code</summary>

```ts
export interface ESLintOptions
    extends Shared.ESLintOptions<ClassicConfig.Config> {
    /**
     * If you pass directory paths to the eslint.lintFiles() method, ESLint checks the files in those directories that
     * have the given extensions. For example, when passing the src/ directory and extensions is [".js", ".ts"], ESLint
     * will lint *.js and *.ts files in src/. If extensions is null, ESLint checks *.js files and files that match
     * overrides[].files patterns in your configuration.
     * Note: This option only applies when you pass directory paths to the eslint.lintFiles() method.
     * If you pass glob patterns, ESLint will lint all files matching the glob pattern regardless of extension.
     */
    extensions?: string[] | null;
    /**
     * If false is present, the eslint.lintFiles() method doesn't respect `.eslintignore` files in your configuration.
     * @default true
     */
    ignore?: boolean;
    /**
     * The path to a file ESLint uses instead of `$CWD/.eslintignore`.
     * If a path is present and the file doesn't exist, this constructor will throw an error.
     */
    ignorePath?: string;
    /**
     * The path to a configuration file, overrides all configurations used with this instance.
     * The options.overrideConfig option is applied after this option is applied.
     */
    overrideConfigFile?: string | null;
    /**
     * The severity to report unused eslint-disable directives.
     * If this option is a severity, it overrides the reportUnusedDisableDirectives setting in your configurations.
     */
    reportUnusedDisableDirectives?: Linter.SeverityString | null;
    /**
     * The path to a directory where plugins should be resolved from.
     * If null is present, ESLint loads plugins from the location of the configuration file that contains the plugin
     * setting.
     * If a path is present, ESLint loads all plugins from there.
     */
    resolvePluginsRelativeTo?: string | null;
    /**
     * An array of paths to directories to load custom rules from.
     */
    rulePaths?: string[];
    /**
     * If false is present, ESLint doesn't load configuration files (.eslintrc.* files).
     * Only the configuration of the constructor options is valid.
     */
    useEslintrc?: boolean;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `extensions` | `string[] | null` | ✓ |  |
| `ignore` | `boolean` | ✓ |  |
| `ignorePath` | `string` | ✓ |  |
| `overrideConfigFile` | `string | null` | ✓ |  |
| `reportUnusedDisableDirectives` | `Linter.SeverityString | null` | ✓ |  |
| `resolvePluginsRelativeTo` | `string | null` | ✓ |  |
| `rulePaths` | `string[]` | ✓ |  |
| `useEslintrc` | `boolean` | ✓ |  |


---

## Type Aliases

### `DeprecatedRuleInfo`

```ts
type DeprecatedRuleInfo = Shared.DeprecatedRuleInfo;
```

### `EditInfo`

```ts
type EditInfo = Shared.EditInfo;
```

### `Formatter`

```ts
type Formatter = Shared.Formatter;
```

### `LintMessage`

```ts
type LintMessage = Shared.LintMessage;
```

### `LintResult`

```ts
type LintResult = Omit<Shared.LintResult, 'stats'>;
```

### `LintTextOptions`

```ts
type LintTextOptions = Shared.LintTextOptions;
```

### `SuppressedLintMessage`

```ts
type SuppressedLintMessage = Shared.SuppressedLintMessage;
```


---