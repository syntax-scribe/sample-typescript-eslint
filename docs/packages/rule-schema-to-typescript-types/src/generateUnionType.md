[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `generateUnionType.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
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
📂 **`packages/rule-schema-to-typescript-types/src/generateUnionType.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `JSONSchema4Type` | `@typescript-eslint/utils/json-schema` |
| `AST` | `./types` |
| `RefMap` | `./types` |
| `UnionAST` | `./types` |
| `NotSupportedError` | `./errors` |
| `generateType` | `./generateType` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `elements` | `AST[]` | const | `[]` | ✗ |


---

## Functions

### `generateUnionType(members: (JSONSchema4 | JSONSchema4Type)[], refMap: RefMap): UnionAST`

<details><summary>Code</summary>

```ts
export function generateUnionType(
  members: (JSONSchema4 | JSONSchema4Type)[],
  refMap: RefMap,
): UnionAST {
  const elements: AST[] = [];

  for (const memberSchema of members) {
    elements.push(
      ((): AST => {
        switch (typeof memberSchema) {
          case 'string':
            return {
              code: `'${memberSchema.replaceAll("'", "\\'")}'`,
              commentLines: [],
              type: 'literal',
            };

          case 'number':
          case 'boolean':
            return {
              code: `${memberSchema}`,
              commentLines: [],
              type: 'literal',
            };

          case 'object':
            if (memberSchema == null) {
              throw new NotSupportedError('null in an enum', memberSchema);
            }
            if (Array.isArray(memberSchema)) {
              throw new NotSupportedError('array in an enum', memberSchema);
            }
            return generateType(memberSchema, refMap);
        }
      })(),
    );
  }

  return {
    commentLines: [],
    elements,
    type: 'union',
  };
}
```
</details>

- **Parameters**:
  - `members: (JSONSchema4 | JSONSchema4Type)[]`
  - `refMap: RefMap`
- **Return Type**: `UnionAST`
- **Calls**:
  - `elements.push`
  - `complex_call_454`
  - `memberSchema.replaceAll`
  - `Array.isArray`
  - `generateType (from ./generateType)`

---