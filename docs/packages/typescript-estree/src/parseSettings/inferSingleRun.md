[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `inferSingleRun.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/typescript-estree/src/parseSettings/inferSingleRun.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `path` | `node:path` |
| `TSESTreeOptions` | `../parser-options` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `possibleEslintBinPaths` | `string[]` | const | `[
      'node_modules/.bin/eslint', // npm or yarn repo
      'node_modules/eslint/bin/eslint.js', // pnpm repo
    ]` | ✗ |


---

## Functions

### `inferSingleRun(options: TSESTreeOptions | undefined): boolean`

<details><summary>Code</summary>

```ts
export function inferSingleRun(options: TSESTreeOptions | undefined): boolean {
  // https://github.com/typescript-eslint/typescript-eslint/issues/9504
  // There's no support (yet?) for extraFileExtensions in single-run hosts.
  // Only watch program hosts and project service can support that.
  if (options?.extraFileExtensions?.length) {
    return false;
  }

  if (
    // single-run implies type-aware linting - no projects means we can't be in single-run mode
    options?.project == null ||
    // programs passed via options means the user should be managing the programs, so we shouldn't
    // be creating our own single-run programs accidentally
    options.programs != null
  ) {
    return false;
  }

  // Allow users to explicitly inform us of their intent to perform a single run (or not) with TSESTREE_SINGLE_RUN
  if (process.env.TSESTREE_SINGLE_RUN === 'false') {
    return false;
  }
  if (process.env.TSESTREE_SINGLE_RUN === 'true') {
    return true;
  }

  // Ideally, we'd like to try to auto-detect CI or CLI usage that lets us infer a single CLI run.
  if (!options.disallowAutomaticSingleRunInference) {
    const possibleEslintBinPaths = [
      'node_modules/.bin/eslint', // npm or yarn repo
      'node_modules/eslint/bin/eslint.js', // pnpm repo
    ];
    if (
      // Default to single runs for CI processes. CI=true is set by most CI providers by default.
      process.env.CI === 'true' ||
      // This will be true for invocations such as `npx eslint ...` and `./node_modules/.bin/eslint ...`
      possibleEslintBinPaths.some(
        binPath =>
          process.argv.length > 1 &&
          process.argv[1].endsWith(path.normalize(binPath)),
      )
    ) {
      return !process.argv.includes('--fix');
    }
  }

  /**
   * We default to assuming that this run could be part of a long-running session (e.g. in an IDE)
   * and watch programs will therefore be required.
   *
   * Unless we can reliably infer otherwise, we default to assuming that this run could be part
   * of a long-running session (e.g. in an IDE) and watch programs will therefore be required
   */
  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * ESLint (and therefore typescript-eslint) is used in both "single run"/one-time contexts,
 * such as an ESLint CLI invocation, and long-running sessions (such as continuous feedback
 * on a file in an IDE).
 *
 * When typescript-eslint handles TypeScript Program management behind the scenes, this distinction
 * is important because there is significant overhead to managing the so called Watch Programs
 * needed for the long-running use-case. We therefore use the following logic to figure out which
 * of these contexts applies to the current execution.
 *
 * @returns Whether this is part of a single run, rather than a long-running process.
 */
```

- **Parameters**:
  - `options: TSESTreeOptions | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `possibleEslintBinPaths.some`
  - `process.argv[1].endsWith`
  - `path.normalize`
  - `process.argv.includes`
- **Internal Comments**:
```
// https://github.com/typescript-eslint/typescript-eslint/issues/9504
// There's no support (yet?) for extraFileExtensions in single-run hosts.
// Only watch program hosts and project service can support that.
// single-run implies type-aware linting - no projects means we can't be in single-run mode (x4)
// programs passed via options means the user should be managing the programs, so we shouldn't (x3)
// be creating our own single-run programs accidentally (x3)
// Allow users to explicitly inform us of their intent to perform a single run (or not) with TSESTREE_SINGLE_RUN
// Ideally, we'd like to try to auto-detect CI or CLI usage that lets us infer a single CLI run.
// Default to single runs for CI processes. CI=true is set by most CI providers by default. (x5)
// This will be true for invocations such as `npx eslint ...` and `./node_modules/.bin/eslint ...` (x3)
/**
   * We default to assuming that this run could be part of a long-running session (e.g. in an IDE)
   * and watch programs will therefore be required.
   *
   * Unless we can reliably infer otherwise, we default to assuming that this run could be part
   * of a long-running session (e.g. in an IDE) and watch programs will therefore be required
   */
```


---