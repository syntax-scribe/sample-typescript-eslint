[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getWrappingFixer.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 18
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

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