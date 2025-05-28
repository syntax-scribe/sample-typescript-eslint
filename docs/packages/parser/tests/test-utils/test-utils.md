[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `test-utils.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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
📂 **`packages/parser/tests/test-utils/test-utils.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/typescript-estree` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `DEFAULT_PARSER_OPTIONS` | `ParserOptions` | const | `{
  comment: true,
  errorOnUnknownASTType: true,
  loc: true,
  range: true,
  raw: true,
  sourceType: 'module',
  tokens: true,
} as const satisfies ParserOptions` | ✗ |


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