[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getDeclaration.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 11 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/type-utils/tests/getDeclaration.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ParserServicesWithTypeInformation` | `@typescript-eslint/typescript-estree` |
| `getDeclaration` | `../src/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `node` | `TSESTree.Node` | const | `{} as TSESTree.Node` | ✗ |


---

## Functions

### `mockSymbol(declarations: ts.Declaration[]): ts.Symbol`

<details><summary>Code</summary>

```ts
(declarations?: ts.Declaration[]): ts.Symbol => {
  return {
    getDeclarations: () => declarations,
  } as ts.Symbol;
}
```
</details>

- **Parameters**:
  - `declarations: ts.Declaration[]`
- **Return Type**: `ts.Symbol`
### `getDeclarations(): ts.Declaration[]`

<details><summary>Code</summary>

```ts
() => declarations
```
</details>

- **Return Type**: `ts.Declaration[]`
### `getDeclarations(): ts.Declaration[]`

<details><summary>Code</summary>

```ts
() => declarations
```
</details>

- **Return Type**: `ts.Declaration[]`
### `getDeclarations(): ts.Declaration[]`

<details><summary>Code</summary>

```ts
() => declarations
```
</details>

- **Return Type**: `ts.Declaration[]`
### `getDeclarations(): ts.Declaration[]`

<details><summary>Code</summary>

```ts
() => declarations
```
</details>

- **Return Type**: `ts.Declaration[]`
### `mockServices(symbol: ts.Symbol): ParserServicesWithTypeInformation`

<details><summary>Code</summary>

```ts
(
  symbol?: ts.Symbol,
): ParserServicesWithTypeInformation => {
  return {
    getSymbolAtLocation: (_: TSESTree.Node) => symbol,
  } as ParserServicesWithTypeInformation;
}
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
- **Return Type**: `ParserServicesWithTypeInformation`
### `getSymbolAtLocation(_: TSESTree.Node): ts.Symbol`

<details><summary>Code</summary>

```ts
(_: TSESTree.Node) => symbol
```
</details>

- **Parameters**:
  - `_: TSESTree.Node`
- **Return Type**: `ts.Symbol`
### `getSymbolAtLocation(_: TSESTree.Node): ts.Symbol`

<details><summary>Code</summary>

```ts
(_: TSESTree.Node) => symbol
```
</details>

- **Parameters**:
  - `_: TSESTree.Node`
- **Return Type**: `ts.Symbol`
### `getSymbolAtLocation(_: TSESTree.Node): ts.Symbol`

<details><summary>Code</summary>

```ts
(_: TSESTree.Node) => symbol
```
</details>

- **Parameters**:
  - `_: TSESTree.Node`
- **Return Type**: `ts.Symbol`
### `getSymbolAtLocation(_: TSESTree.Node): ts.Symbol`

<details><summary>Code</summary>

```ts
(_: TSESTree.Node) => symbol
```
</details>

- **Parameters**:
  - `_: TSESTree.Node`
- **Return Type**: `ts.Symbol`
### `mockDeclaration(): ts.Declaration`

<details><summary>Code</summary>

```ts
(): ts.Declaration => {
  return {} as ts.Declaration;
}
```
</details>

- **Return Type**: `ts.Declaration`

---