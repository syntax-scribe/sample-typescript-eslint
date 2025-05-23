[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ajv.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/ajv.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Ajv` | `ajv` |
| `metaSchema` | `ajv/lib/refs/json-schema-draft-04.json` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---