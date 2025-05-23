[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 2
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/website/src/components/linter/types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `analyze` | `@typescript-eslint/scope-manager` |
| `ScopeManager` | `@typescript-eslint/scope-manager` |
| `astConverter` | `@typescript-eslint/typescript-estree/use-at-your-own-risk` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ClassicConfig` | `@typescript-eslint/utils/ts-eslint` |
| `Linter` | `@typescript-eslint/utils/ts-eslint` |
| `SourceCode` | `@typescript-eslint/utils/ts-eslint` |
| `esquery` | `esquery` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `UpdateModel`

<details><summary>Interface Code</summary>

```ts
export interface UpdateModel {
  storedAST?: TSESTree.Program;
  storedScope?: ScopeManager;
  storedTsAST?: ts.Node;
  typeChecker?: ts.TypeChecker;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `storedAST` | `TSESTree.Program` | ✓ |  |
| `storedScope` | `ScopeManager` | ✓ |  |
| `storedTsAST` | `ts.Node` | ✓ |  |
| `typeChecker` | `ts.TypeChecker` | ✓ |  |

### `WebLinterModule`

<details><summary>Interface Code</summary>

```ts
export interface WebLinterModule {
  analyze: typeof analyze;
  astConverter: typeof astConverter;
  configs: Record<string, ClassicConfig.Config>;
  createLinter: () => Linter;
  esquery: typeof esquery;
  visitorKeys: SourceCode.VisitorKeys;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `analyze` | `typeof analyze` | ✗ |  |
| `astConverter` | `typeof astConverter` | ✗ |  |
| `configs` | `Record<string, ClassicConfig.Config>` | ✗ |  |
| `createLinter` | `() => Linter` | ✗ |  |
| `esquery` | `typeof esquery` | ✗ |  |
| `visitorKeys` | `SourceCode.VisitorKeys` | ✗ |  |


---

## Type Aliases

### `PlaygroundSystem`

```ts
type PlaygroundSystem = {
  removeFile: (fileName: string) => void;
  searchFiles: (path: string) => string[];
} & Required<Pick<ts.System, 'deleteFile' | 'watchFile'>> &
  ts.System;
```

### `LinterOnLint`

```ts
type LinterOnLint = (
  fileName: string,
  messages: Linter.LintMessage[],
) => void;
```

### `LinterOnParse`

```ts
type LinterOnParse = (fileName: string, model: UpdateModel) => void;
```


---