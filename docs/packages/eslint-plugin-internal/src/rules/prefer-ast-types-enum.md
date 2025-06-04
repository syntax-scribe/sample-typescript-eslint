[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-ast-types-enum.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 10 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/prefer-ast-types-enum.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `value` | `any` | const | `node.value` | ✗ |


---

## Functions

### `isStringLiteral(node: TSESTree.Literal): node is TSESTree.StringLiteral`

<details><summary>Code</summary>

```ts
(
  node: TSESTree.Literal,
): node is TSESTree.StringLiteral => typeof node.value === 'string'
```
</details>

- **Parameters**:
  - `node: TSESTree.Literal`
- **Return Type**: `node is TSESTree.StringLiteral`
### `report(enumName: 'AST_NODE_TYPES' | 'AST_TOKEN_TYPES' | 'DefinitionType', literal: TSESTree.StringLiteral): void`

<details><summary>Code</summary>

```ts
(
      enumName: 'AST_NODE_TYPES' | 'AST_TOKEN_TYPES' | 'DefinitionType',
      literal: TSESTree.StringLiteral,
    ): void =>
      context.report({
        node: literal,
        messageId: 'preferEnum',
        data: { enumName, literal: literal.value },
        fix: fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`),
      })
```
</details>

- **Parameters**:
  - `enumName: 'AST_NODE_TYPES' | 'AST_TOKEN_TYPES' | 'DefinitionType'`
  - `literal: TSESTree.StringLiteral`
- **Return Type**: `void`
- **Calls**:
  - `context.report`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.replaceText(literal, `${enumName}.${literal.value}`)
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.replaceText`

---