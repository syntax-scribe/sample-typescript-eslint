[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `schemas.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 10 |
| ⚡ Async/Await Patterns | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/schemas.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `compile` | `@typescript-eslint/rule-schema-to-typescript-types` |
| `prettier` | `prettier` |
| `rules` | `../src/rules/index.js` |
| `areOptionsValid` | `./areOptionsValid.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `config` | `any` | let/var | `await prettier.resolveConfig(filepath, {
    config: PRETTIER_CONFIG_PATH,
  })` | ✗ |
| `SKIPPED_RULES_FOR_TYPE_GENERATION` | `Set<string>` | const | `new Set(['indent'])` | ✗ |
| `ONLY` | `""` | const | `''` | ✗ |
| `PRETTIER_CONFIG` | `{ schema: prettier.Options; tsType: Promise<prettier.Options>; }` | let/var | `{
    schema: await getPrettierConfig(SCHEMA_FILEPATH),
    tsType: getPrettierConfig(TS_TYPE_FILEPATH),
  }` | ✗ |
| `schemaString` | `any` | let/var | `await prettier.format(
        JSON.stringify(
          ruleDef.meta.schema,
          (k, v: unknown) => {
            if (k === 'enum' && Array.isArray(v)) {
              // sort enum arrays for consistency regardless of source order
              v.sort();
            } else if (
              typeof v === 'object' &&
              v != null &&
              !Array.isArray(v)
            ) {
              // sort properties for consistency regardless of source order
              return Object.fromEntries(
                Object.entries(v).sort(([a], [b]) => a.localeCompare(b)),
              );
            }
            return v;
          },
          // use the indent feature as it forces all objects to be multiline
          // if we don't do this then prettier decides what objects are multiline
          // based on what fits on a line - which looks less consistent
          // and makes changes harder to understand as you can have multiple
          // changes per line, or adding a prop can restructure an object
          2,
        ),
        PRETTIER_CONFIG.schema,
      )` | ✗ |
| `compilationResult` | `any` | let/var | `await compile(
        ruleDef.meta.schema,
        PRETTIER_CONFIG.tsType,
      )` | ✗ |
| `files` | `string[]` | let/var | `await fs.readdir(snapshotFolder, { encoding: 'utf-8' })` | ✗ |
| `names` | `Set<string>` | let/var | `new Set(
    ruleEntries
      .filter(([k]) => !SKIPPED_RULES_FOR_TYPE_GENERATION.has(k))
      .map(([k]) => `${k}.shot`),
  )` | ✗ |
| `VALID_SCHEMA_PROPS` | `Set<"type" | "id" | "properties" | "extends" | "default" | "additionalProperties" | "enum" | "required" | "items" | "description" | "format" | "$defs" | "$ref" | "$schema" | "additionalItems" | ... 20 more ... | "uniqueItems">` | const | `new Set([
  '$defs',
  '$ref',
  '$schema',
  'additionalItems',
  'additionalProperties',
  'allOf',
  'anyOf',
  'default',
  'definitions',
  'dependencies',
  'description',
  'enum',
  'exclusiveMaximum',
  'exclusiveMinimum',
  'extends',
  'format',
  'id',
  'items',
  'maximum',
  'maxItems',
  'maxLength',
  'maxProperties',
  'minimum',
  'minItems',
  'minLength',
  'minProperties',
  'multipleOf',
  'not',
  'oneOf',
  'pattern',
  'patternProperties',
  'properties',
  'required',
  'title',
  'type',
  'uniqueItems',
] as const)` | ✗ |
| `overrideValidOptions` | `Record<string, unknown>` | const | `{
    'func-call-spacing': ['never'],
    semi: ['never'],
  }` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `getPrettierConfig` | prettier.resolveConfig(filepath, {
    config: PRETTIER_CONFIG_PATH,
  }) | *none* |


---

## Functions

### `getPrettierConfig(filepath: string): Promise<prettier.Options>`

<details><summary>Code</summary>

```ts
async (
  filepath: string,
): Promise<prettier.Options> => {
  const config = await prettier.resolveConfig(filepath, {
    config: PRETTIER_CONFIG_PATH,
  });
  if (config == null) {
    throw new Error('Unable to resolve prettier config');
  }
  return {
    ...config,
    filepath,
  };
}
```
</details>

- **Parameters**:
  - `filepath: string`
- **Return Type**: `Promise<prettier.Options>`
- **Calls**:
  - `prettier.resolveConfig`

---