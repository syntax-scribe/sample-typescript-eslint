[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `areOptionsValid.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
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
📂 **`packages/eslint-plugin/tests/areOptionsValid.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `JSONSchema4` | `json-schema` |
| `TSUtils` | `@typescript-eslint/utils` |
| `Ajv` | `ajv` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ajv` | `any` | const | `new Ajv({ async: false })` | ✗ |


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