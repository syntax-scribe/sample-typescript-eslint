[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `prefer-optional-chain.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 112 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/prefer-optional-chain/prefer-optional-chain.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `noFormat` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../../src/rules/prefer-optional-chain` |
| `dedupeTestCases` | `../../dedupeTestCases` |
| `getFixturesRootDir` | `../../RuleTester` |
| `BaseCases` | `./base-cases` |
| `identity` | `./base-cases` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: getFixturesRootDir(),
    },
  },
})` | ✗ |


---

## Functions

### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing.bong;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing.bong;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing.bong;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' && bing.bong;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= null &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!== undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('&&', '!= undefined &&')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c.replaceAll('||', '|| !')}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c.replaceAll('||', '|| !')}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c.replaceAll('||', '|| !')}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c.replaceAll('||', '|| !')}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => `!${c}`
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== null ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== null ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== null ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== null ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| undefined', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== null ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == null;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== undefined ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== undefined ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== undefined ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('||', '=== undefined ||')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '=== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateDeclaration(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('| null', '')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' === undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c =>
              c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c
                .replaceAll('||', '== undefined ||')
                // SEE TODO AT THE BOTTOM OF THE RULE
                // We need to ensure the final operand is also a "valid" `||` check
                .replace`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replace(/;$/, ' == undefined;')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replace`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.      ')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.      '))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.      ')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.      '))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.\n')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.\n'))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.\n')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.\n'))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.      ')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.      '))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.      ')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.      '))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.\n')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.\n'))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateCode(c: string): string`

<details><summary>Code</summary>

```ts
c => c.replaceAll('.', '.\n')
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`
### `mutateOutput(c: string): string`

<details><summary>Code</summary>

```ts
c =>
            c.replaceAll(/(\[.+])/g, m => m.replaceAll('.', '.\n'))
```
</details>

- **Parameters**:
  - `c: string`
- **Return Type**: `string`
- **Calls**:
  - `c.replaceAll`

---