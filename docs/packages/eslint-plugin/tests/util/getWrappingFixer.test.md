[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappingFixer.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 66 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
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
📂 **`packages/eslint-plugin/tests/util/getWrappingFixer.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `createRule` | `../../src/util` |
| `getWrappingFixer` | `../../src/util` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |


---

## Functions

### `report(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.Node): void => {
      context.report({
        fix: getWrappingFixer({
          node,
          sourceCode: context.sourceCode,
          wrap: code => `void ${code.replaceAll('wrap', 'wrapped')}`,
        }),
        messageId: 'addVoid',
        node,
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getWrappingFixer (from ../../src/util)`
  - `code.replaceAll`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => `void ${code.replaceAll('wrap', 'wrapped')}`
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `report(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.CallExpression): void => {
      context.report({
        fix: getWrappingFixer({
          innerNode: [node.arguments[0]],
          node,
          sourceCode: context.sourceCode,
          wrap: code => code,
        }),
        messageId: 'removeFunction',
        node,
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
  - `getWrappingFixer (from ../../src/util)`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `wrap(code: string): string`

<details><summary>Code</summary>

```ts
code => code
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`

---