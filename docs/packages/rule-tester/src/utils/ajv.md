[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ajv.ts`

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
📂 **`packages/rule-tester/src/utils/ajv.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Ajv` | `ajv` |
| `metaSchema` | `ajv/lib/refs/json-schema-draft-04.json` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ajv` | `any` | const | `new Ajv({
    meta: false,
    missingRefs: 'ignore',
    schemaId: 'auto',
    useDefaults: true,
    validateSchema: false,
    verbose: true,
    ...additionalOptions,
  })` | ✗ |


---

## Functions

### `ajvBuilder(additionalOptions: {}): Ajv.Ajv`

<details><summary>Code</summary>

```ts
export function ajvBuilder(additionalOptions = {}): Ajv.Ajv {
  const ajv = new Ajv({
    meta: false,
    missingRefs: 'ignore',
    schemaId: 'auto',
    useDefaults: true,
    validateSchema: false,
    verbose: true,
    ...additionalOptions,
  });

  ajv.addMetaSchema(metaSchema);

  // @ts-expect-error -- this is an untyped part of the ajv API
  ajv._opts.defaultMeta = metaSchema.id;

  return ajv;
}
```
</details>

- **Parameters**:
  - `additionalOptions: {}`
- **Return Type**: `Ajv.Ajv`
- **Calls**:
  - `ajv.addMetaSchema`
- **Internal Comments**:
```
// @ts-expect-error -- this is an untyped part of the ajv API (x5)
```


---