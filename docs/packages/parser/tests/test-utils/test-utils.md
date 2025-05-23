[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `test-utils.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/parser/tests/test-utils/test-utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/typescript-estree` |


---

## Functions

### `createConfig(filename: string): ParserOptions`

<details><summary>Code</summary>

```ts
export function createConfig(filename: string): ParserOptions {
  return {
    ...DEFAULT_PARSER_OPTIONS,
    filePath: filename,
    project: './tsconfig.json',
    tsconfigRootDir: FIXTURES_DIR,
  };
}
```
</details>

- **Parameters**:
  - `filename: string`
- **Return Type**: `ParserOptions`
### `getRaw(ast: TSESTree.Program): TSESTree.Program`

<details><summary>Code</summary>

```ts
export function getRaw(ast: TSESTree.Program): TSESTree.Program {
  return JSON.parse(
    JSON.stringify(ast, (key, value) => {
      if ((key === 'start' || key === 'end') && typeof value === 'number') {
        return undefined;
      }
      return value;
    }),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Returns a raw copy of the given AST
 * @param ast the AST object
 * @returns copy of the AST object
 */
```

- **Parameters**:
  - `ast: TSESTree.Program`
- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `JSON.parse`
  - `JSON.stringify`

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