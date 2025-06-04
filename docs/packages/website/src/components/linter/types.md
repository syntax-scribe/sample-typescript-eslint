[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 1 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 3 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

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

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `@typescript-eslint/typescript-estree/use-at-your-own-risk` | ParseSettings |


---


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