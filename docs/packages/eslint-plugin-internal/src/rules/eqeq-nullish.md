[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `eqeq-nullish.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 16 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/src/rules/eqeq-nullish.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `nullThrows` | `@typescript-eslint/utils/eslint-utils` |
| `NullThrowsReasons` | `@typescript-eslint/utils/eslint-utils` |
| `createRule` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `wasLeft` | `boolean` | const | `node.left === offendingChild` | ✗ |
| `nullishKind` | `"undefined" | "null"` | const | `offendingChild.type === AST_NODE_TYPES.Identifier
              ? 'undefined'
              : 'null'` | ✗ |
| `looseOperator` | `"==" | "!="` | const | `node.operator === '===' ? '==' : '!='` | ✗ |


---

## Functions

### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`
### `fix(fixer: any): any[]`

<details><summary>Code</summary>

```ts
fixer => [
                  fixer.replaceText(offendingChild, 'null'),
                  fixer.replaceText(operatorToken, looseOperator),
                ]
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any[]`

---