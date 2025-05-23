[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `areOptionsValid.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/areOptionsValid.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `JSONSchema4` | `json-schema` |
| `TSUtils` | `@typescript-eslint/utils` |
| `Ajv` | `ajv` |


---

## Functions

### `areOptionsValid(rule: RuleModule<string, readonly unknown[]>, options: unknown): boolean`

<details><summary>Code</summary>

```ts
export function areOptionsValid(
  rule: RuleModule<string, readonly unknown[]>,
  options: unknown,
): boolean {
  const normalizedSchema = normalizeSchema(rule.meta.schema);

  const valid = ajv.validate(normalizedSchema, options);
  if (typeof valid !== 'boolean') {
    // Schema could not validate options synchronously. This is not allowed for ESLint rules.
    return false;
  }

  return valid;
}
```
</details>

- **Parameters**:
  - `rule: RuleModule<string, readonly unknown[]>`
  - `options: unknown`
- **Return Type**: `boolean`
- **Calls**:
  - `normalizeSchema`
  - `ajv.validate`
- **Internal Comments**:
```
// Schema could not validate options synchronously. This is not allowed for ESLint rules.
```

### `normalizeSchema(schema: JSONSchema4 | readonly JSONSchema4[]): JSONSchema4`

<details><summary>Code</summary>

```ts
function normalizeSchema(
  schema: JSONSchema4 | readonly JSONSchema4[],
): JSONSchema4 {
  if (!TSUtils.isArray(schema)) {
    return schema;
  }

  if (schema.length === 0) {
    return {
      maxItems: 0,
      minItems: 0,
      type: 'array',
    };
  }

  return {
    items: schema as JSONSchema4[],
    maxItems: schema.length,
    minItems: 0,
    type: 'array',
  };
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4 | readonly JSONSchema4[]`
- **Return Type**: `JSONSchema4`
- **Calls**:
  - `TSUtils.isArray`

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