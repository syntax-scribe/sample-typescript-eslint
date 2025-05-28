[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 6 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 1 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-schema-to-typescript-types/src/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `TSUtils` | `@typescript-eslint/utils` |
| `prettier` | `prettier` |
| `AST` | `./types` |
| `generateType` | `./generateType` |
| `optimizeAST` | `./optimizeAST` |
| `printTypeAlias` | `./printAST` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `refTypes` | `string[]` | let/var | `[]` | ✗ |
| `types` | `AST[]` | let/var | `[]` | ✗ |
| `optionsType` | `string` | let/var | `isArraySchema
    ? printTypeAlias('Options', {
        commentLines: [],
        elements: types,
        spreadType: null,
        type: 'tuple',
      })
    : printTypeAlias('Options', types[0])` | ✗ |
| `refTypes` | `string[]` | const | `[]` | ✗ |
| `refMap` | `Map<string, string>` | const | `new Map<string, string>()` | ✗ |
| `defs` | `any` | const | `schema.$defs ?? schema.definitions` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| async-function | `compile` | prettier.format(unformattedCode, await prettierConfig), prettierConfig | *none* |


---

## Functions

### `compile(schemaIn: JSONSchema4 | readonly JSONSchema4[], prettierConfig: Promise<prettier.Options>): Promise<string>`

<details><summary>Code</summary>

```ts
export async function compile(
  schemaIn: JSONSchema4 | readonly JSONSchema4[],
  prettierConfig: Promise<prettier.Options>,
): Promise<string> {
  const { isArraySchema, schema } = (() => {
    if (TSUtils.isArray(schemaIn)) {
      return {
        isArraySchema: true,
        schema: schemaIn,
      };
    }
    return {
      isArraySchema: false,
      schema: [schemaIn],
    };
  })();

  if (schema.length === 0) {
    return ['/** No options declared */', 'type Options = [];'].join('\n');
  }

  const refTypes: string[] = [];
  const types: AST[] = [];
  for (let i = 0; i < schema.length; i += 1) {
    const result = compileSchema(schema[i], i);
    refTypes.push(...result.refTypes);
    types.push(result.type);
  }

  const optionsType = isArraySchema
    ? printTypeAlias('Options', {
        commentLines: [],
        elements: types,
        spreadType: null,
        type: 'tuple',
      })
    : printTypeAlias('Options', types[0]);

  const unformattedCode = [...refTypes, optionsType].join('\n\n');
  try {
    return await prettier.format(unformattedCode, await prettierConfig);
  } catch (e) {
    if (e instanceof Error) {
      e.message += `\n\nUnformatted Code:\n${unformattedCode}`;
    }
    throw e;
  }
}
```
</details>

- **Parameters**:
  - `schemaIn: JSONSchema4 | readonly JSONSchema4[]`
  - `prettierConfig: Promise<prettier.Options>`
- **Return Type**: `Promise<string>`
- **Calls**:
  - `complex_call_518`
  - `TSUtils.isArray`
  - `['/** No options declared */', 'type Options = [];'].join`
  - `compileSchema`
  - `refTypes.push`
  - `types.push`
  - `printTypeAlias (from ./printAST)`
  - `[...refTypes, optionsType].join`
  - `prettier.format`
### `compileSchema(schema: JSONSchema4, index: number): { refTypes: string[]; type: AST }`

<details><summary>Code</summary>

```ts
function compileSchema(
  schema: JSONSchema4,
  index: number,
): { refTypes: string[]; type: AST } {
  const refTypes: string[] = [];

  const refMap = new Map<string, string>();
  // we only support defs at the top level for simplicity
  const defs = schema.$defs ?? schema.definitions;
  if (defs) {
    for (const [defKey, defSchema] of Object.entries(defs)) {
      const typeName = toPascalCase(defKey);
      refMap.set(`#/$defs/${defKey}`, typeName);
      refMap.set(`#/items/${index}/$defs/${defKey}`, typeName);

      const type = generateType(defSchema, refMap);
      optimizeAST(type);
      refTypes.push(printTypeAlias(typeName, type));
    }
  }

  const type = generateType(schema, refMap);
  optimizeAST(type);

  return {
    refTypes,
    type,
  };
}
```
</details>

- **Parameters**:
  - `schema: JSONSchema4`
  - `index: number`
- **Return Type**: `{ refTypes: string[]; type: AST }`
- **Calls**:
  - `Object.entries`
  - `toPascalCase`
  - `refMap.set`
  - `generateType (from ./generateType)`
  - `optimizeAST (from ./optimizeAST)`
  - `refTypes.push`
  - `printTypeAlias (from ./printAST)`
- **Internal Comments**:
```
// we only support defs at the top level for simplicity (x2)
```

### `toPascalCase(key: string): string`

<details><summary>Code</summary>

```ts
function toPascalCase(key: string): string {
  return key[0].toUpperCase() + key.substring(1);
}
```
</details>

- **Parameters**:
  - `key: string`
- **Return Type**: `string`
- **Calls**:
  - `key[0].toUpperCase`
  - `key.substring`

---