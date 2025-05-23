[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `index.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---