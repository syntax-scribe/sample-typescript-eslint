[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `config-helper.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 5 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/typescript-eslint/src/config-helper.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `config` | `{ name?: unknown; extends?: unknown; files?: unknown; ignores?: unknown; }` | const | `_config as {
        name?: unknown;
        extends?: unknown;
        files?: unknown;
        ignores?: unknown;
      }` | ✗ |
| `nameErrorPhrase` | `string` | const | `name != null ? `, named "${name}",` : ' (anonymous)'` | ✗ |
| `nonObjectExtensions` | `any[]` | const | `[]` | ✗ |
| `configArray` | `any[]` | const | `[]` | ✗ |
| `extension` | `{ name?: unknown; files?: unknown; ignores?: unknown; }` | const | `_extension as {
          name?: unknown;
          files?: unknown;
          ignores?: unknown;
        }` | ✗ |


---

## Functions

### `config(configs: InfiniteDepthConfigWithExtends[]): ConfigArray`

<details><summary>Code</summary>

```ts
export function config(
  ...configs: InfiniteDepthConfigWithExtends[]
): ConfigArray {
  return configImpl(...configs);
}
```
</details>

- **JSDoc**:
```ts
/**
 * Utility function to make it easy to strictly type your "Flat" config file
 * @example
 * ```js
 * // @ts-check
 *
 * import eslint from '@eslint/js';
 * import tseslint from 'typescript-eslint';
 *
 * export default tseslint.config(
 *   eslint.configs.recommended,
 *   tseslint.configs.recommended,
 *   {
 *     rules: {
 *       '@typescript-eslint/array-type': 'error',
 *     },
 *   },
 * );
 * ```
 */
```

- **Parameters**:
  - `configs: InfiniteDepthConfigWithExtends[]`
- **Return Type**: `ConfigArray`
- **Calls**:
  - `configImpl`
### `configImpl(configs: unknown[]): ConfigArray`

<details><summary>Code</summary>

```ts
function configImpl(...configs: unknown[]): ConfigArray {
  const flattened = configs.flat(Infinity);
  return flattened.flatMap(
    (
      configWithExtends,
      configIndex,
    ): TSESLint.FlatConfig.Config | TSESLint.FlatConfig.Config[] => {
      if (
        configWithExtends == null ||
        typeof configWithExtends !== 'object' ||
        !('extends' in configWithExtends)
      ) {
        // Unless the object is a config object with extends key, just forward it
        // along to eslint.
        return configWithExtends as TSESLint.FlatConfig.Config;
      }

      const { extends: extendsArr, ..._config } = configWithExtends;
      const config = _config as {
        name?: unknown;
        extends?: unknown;
        files?: unknown;
        ignores?: unknown;
      };

      if (extendsArr == null) {
        // If the extends value is nullish, just forward along the rest of the
        // config object to eslint.
        return config as TSESLint.FlatConfig.Config;
      }

      const name = ((): string | undefined => {
        if ('name' in configWithExtends && configWithExtends.name != null) {
          if (typeof configWithExtends.name !== 'string') {
            throw new Error(
              `tseslint.config(): Config at index ${configIndex} has a 'name' property that is not a string.`,
            );
          }
          return configWithExtends.name;
        }
        return undefined;
      })();
      const nameErrorPhrase =
        name != null ? `, named "${name}",` : ' (anonymous)';

      if (!Array.isArray(extendsArr)) {
        throw new TypeError(
          `tseslint.config(): Config at index ${configIndex}${nameErrorPhrase} has an 'extends' property that is not an array.`,
        );
      }

      const extendsArrFlattened = (extendsArr as unknown[]).flat(Infinity);

      const nonObjectExtensions = [];
      for (const [extensionIndex, extension] of extendsArrFlattened.entries()) {
        // special error message to be clear we don't support eslint's stringly typed extends.
        // https://eslint.org/docs/latest/use/configure/configuration-files#extending-configurations
        if (typeof extension === 'string') {
          throw new Error(
            `tseslint.config(): Config at index ${configIndex}${nameErrorPhrase} has an 'extends' array that contains a string (${JSON.stringify(extension)}) at index ${extensionIndex}.` +
              " This is a feature of eslint's `defineConfig()` helper and is not supported by typescript-eslint." +
              ' Please provide a config object instead.',
          );
        }
        if (extension == null || typeof extension !== 'object') {
          nonObjectExtensions.push(extensionIndex);
        }
      }
      if (nonObjectExtensions.length > 0) {
        const extensionIndices = nonObjectExtensions.join(', ');
        throw new Error(
          `tseslint.config(): Config at index ${configIndex}${nameErrorPhrase} contains non-object` +
            ` extensions at the following indices: ${extensionIndices}.`,
        );
      }

      const configArray = [];

      for (const _extension of extendsArrFlattened) {
        const extension = _extension as {
          name?: unknown;
          files?: unknown;
          ignores?: unknown;
        };
        const resolvedConfigName = [name, extension.name]
          .filter(Boolean)
          .join('__');
        if (isPossiblyGlobalIgnores(extension)) {
          // If it's a global ignores, then just pass it along
          configArray.push({
            ...extension,
            ...(resolvedConfigName !== '' ? { name: resolvedConfigName } : {}),
          });
        } else {
          configArray.push({
            ...extension,
            ...(config.files ? { files: config.files } : {}),
            ...(config.ignores ? { ignores: config.ignores } : {}),
            ...(resolvedConfigName !== '' ? { name: resolvedConfigName } : {}),
          });
        }
      }

      // If the base config could form a global ignores object, then we mustn't include
      // it in the output. Otherwise, we must add it in order for it to have effect.
      if (!isPossiblyGlobalIgnores(config)) {
        configArray.push(config);
      }

      return configArray as ConfigArray;
    },
  );
}
```
</details>

- **Parameters**:
  - `configs: unknown[]`
- **Return Type**: `ConfigArray`
- **Calls**:
  - `configs.flat`
  - `flattened.flatMap`
  - `complex_call_3810`
  - `Array.isArray`
  - `(extendsArr as unknown[]).flat`
  - `extendsArrFlattened.entries`
  - `JSON.stringify`
  - `nonObjectExtensions.push`
  - `nonObjectExtensions.join`
  - `[name, extension.name]
          .filter(Boolean)
          .join`
  - `isPossiblyGlobalIgnores`
  - `configArray.push`
- **Internal Comments**:
```
// Unless the object is a config object with extends key, just forward it
// along to eslint.
// If the extends value is nullish, just forward along the rest of the
// config object to eslint.
// special error message to be clear we don't support eslint's stringly typed extends.
// https://eslint.org/docs/latest/use/configure/configuration-files#extending-configurations
// If it's a global ignores, then just pass it along (x4)
// If the base config could form a global ignores object, then we mustn't include
// it in the output. Otherwise, we must add it in order for it to have effect.
```

### `isPossiblyGlobalIgnores(config: object): boolean`

<details><summary>Code</summary>

```ts
function isPossiblyGlobalIgnores(config: object): boolean {
  return Object.keys(config).every(key => ['name', 'ignores'].includes(key));
}
```
</details>

- **JSDoc**:
```ts
/**
 * This utility function returns false if the config objects contains any field
 * that would prevent it from being considered a global ignores object and true
 * otherwise. Note in particular that the `ignores` field may not be present and
 * the return value can still be true.
 */
```

- **Parameters**:
  - `config: object`
- **Return Type**: `boolean`
- **Calls**:
  - `Object.keys(config).every`
  - `['name', 'ignores'].includes`

---

## Interfaces

### `ConfigWithExtends`

<details><summary>Interface Code</summary>

```ts
export interface ConfigWithExtends extends TSESLint.FlatConfig.Config {
  /**
   * Allows you to "extend" a set of configs similar to `extends` from the
   * classic configs.
   *
   * This is just a convenience short-hand to help reduce duplication.
   *
   * ```js
   * export default tseslint.config({
   *   files: ['** /*.ts'],
   *   extends: [
   *     eslint.configs.recommended,
   *     tseslint.configs.recommended,
   *   ],
   *   rules: {
   *     '@typescript-eslint/array-type': 'error',
   *     '@typescript-eslint/consistent-type-imports': 'error',
   *   },
   * })
   *
   * // expands to
   *
   * export default [
   *   {
   *     ...eslint.configs.recommended,
   *     files: ['** /*.ts'],
   *   },
   *   ...tseslint.configs.recommended.map(conf => ({
   *     ...conf,
   *     files: ['** /*.ts'],
   *   })),
   *   {
   *     files: ['** /*.ts'],
   *     rules: {
   *       '@typescript-eslint/array-type': 'error',
   *       '@typescript-eslint/consistent-type-imports': 'error',
   *     },
   *   },
   * ]
   * ```
   */
  extends?: InfiniteDepthConfigWithExtends[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `extends` | `InfiniteDepthConfigWithExtends[]` | ✓ |  |


---

## Type Aliases

### `InfiniteDepthConfigWithExtends`

```ts
type InfiniteDepthConfigWithExtends = | ConfigWithExtends
  | InfiniteDepthConfigWithExtends[];
```

### `ConfigArray`

```ts
type ConfigArray = TSESLint.FlatConfig.ConfigArray;
```


---