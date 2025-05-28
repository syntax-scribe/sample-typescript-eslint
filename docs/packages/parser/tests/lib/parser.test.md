[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `parser.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 8 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 13 |
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
📂 **`packages/parser/tests/lib/parser.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserOptions` | `@typescript-eslint/types` |
| `ScriptTarget` | `typescript` |
| `parse` | `../../src/parser.js` |
| `parseForESLint` | `../../src/parser.js` |
| `FIXTURES_DIR` | `../test-utils/test-utils.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `config` | `ParserOptions` | const | `{
      ecmaFeatures: {
        globalReturn: false,
        jsx: false,
      },
      sourceType: 'module' as const,
      // ts-estree specific
      errorOnTypeScriptSyntacticAndSemanticIssues: false,
      extraFileExtensions: ['.foo'],
      filePath: './isolated-file.src.ts',
      project: 'tsconfig.json',
      tsconfigRootDir: FIXTURES_DIR,
    }` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `config` | `ParserOptions` | const | `{
      errorOnTypeScriptSyntacticAndSemanticIssues: false,
      filePath: 'isolated-file.src.ts',
      project: 'tsconfig.json',
      tsconfigRootDir: FIXTURES_DIR,
    }` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `config` | `ParserOptions` | const | `{
        filePath: 'isolated-file.src.ts',
        project: 'tsconfig.json',
        tsconfigRootDir: FIXTURES_DIR,
      }` | ✗ |
| `code` | `"const valid = true;"` | const | `'const valid = true;'` | ✗ |
| `config` | `ParserOptions` | const | `{
      ecmaFeatures: {
        globalReturn: false,
        jsx: false,
      },
      sourceType: 'module' as const,
      // scope-manager specific
      jsxFragmentName: 'Bar',
      jsxPragma: 'Foo',
      lib: ['dom.iterable'],
      // ts-estree specific
      errorOnTypeScriptSyntacticAndSemanticIssues: false,
      extraFileExtensions: ['.foo'],
      filePath: 'isolated-file.src.ts',
      project: 'tsconfig.json',
      tsconfigRootDir: FIXTURES_DIR,
    }` | ✗ |


---

## Functions

### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`
### `getCompilerOptions(): { target: any; }`

<details><summary>Code</summary>

```ts
() => ({ target })
```
</details>

- **Return Type**: `{ target: any; }`

---