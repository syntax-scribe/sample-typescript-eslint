[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getRuleOptionsSchema.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
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
📂 **`packages/rule-tester/src/utils/getRuleOptionsSchema.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `AnyRuleModule` | `@typescript-eslint/utils/ts-eslint` |
| `isReadonlyArray` | `./isReadonlyArray` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `schema` | `any` | const | `rule.meta?.schema` | ✗ |


---

## Functions

### `getRuleOptionsSchema(rule: Partial<AnyRuleModule>): JSONSchema4 | null`

<details><summary>Code</summary>

```ts
export function getRuleOptionsSchema(
  rule: Partial<AnyRuleModule>,
): JSONSchema4 | null {
  const schema = rule.meta?.schema;

  // Given a tuple of schemas, insert warning level at the beginning
  if (isReadonlyArray(schema)) {
    if (schema.length) {
      return {
        items: schema as JSONSchema4[],
        maxItems: schema.length,
        minItems: 0,
        type: 'array',
      };
    }
    return {
      maxItems: 0,
      minItems: 0,
      type: 'array',
    };
  }

  // Given a full schema, leave it alone
  return schema ?? null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets a complete options schema for a rule.
 * @param rule A new-style rule object
 * @returns JSON Schema for the rule's options.
 */
```

- **Parameters**:
  - `rule: Partial<AnyRuleModule>`
- **Return Type**: `JSONSchema4 | null`
- **Calls**:
  - `isReadonlyArray (from ./isReadonlyArray)`
- **Internal Comments**:
```
// Given a tuple of schemas, insert warning level at the beginning
// Given a full schema, leave it alone
```


---