[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 1 |
| 📐 Interfaces | 4 |
| 📑 Type Aliases | 9 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |


---

## Interfaces

### `RuleDetails`

<details><summary>Interface Code</summary>

```ts
export interface RuleDetails {
  description?: string;
  name: string;
  url?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `description` | `string` | ✓ |  |
| `name` | `string` | ✗ |  |
| `url` | `string` | ✓ |  |

### `ConfigModel`

<details><summary>Interface Code</summary>

```ts
export interface ConfigModel {
  code: string;
  eslintrc: string;
  esQuery?: {
    filter?: string;
    selector: ESQuery.Selector;
  };
  fileType?: ConfigFileType;
  scroll?: boolean;
  showAST?: ConfigShowAst;
  showTokens?: boolean;
  sourceType?: SourceType;
  ts: string;
  tsconfig: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `eslintrc` | `string` | ✗ |  |
| `esQuery` | `{
    filter?: string;
    selector: ESQuery.Selector;
  }` | ✓ |  |
| `fileType` | `ConfigFileType` | ✓ |  |
| `scroll` | `boolean` | ✓ |  |
| `showAST` | `ConfigShowAst` | ✓ |  |
| `showTokens` | `boolean` | ✓ |  |
| `sourceType` | `SourceType` | ✓ |  |
| `ts` | `string` | ✗ |  |
| `tsconfig` | `string` | ✗ |  |

### `ErrorItem`

<details><summary>Interface Code</summary>

```ts
export interface ErrorItem {
  fixer?: { fix(): void; message: string };
  location: string;
  message: string;
  severity: number;
  suggestions: { fix(): void; message: string }[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `fixer` | `{ fix(): void; message: string }` | ✓ |  |
| `location` | `string` | ✗ |  |
| `message` | `string` | ✗ |  |
| `severity` | `number` | ✗ |  |
| `suggestions` | `{ fix(): void; message: string }[]` | ✗ |  |

### `ErrorGroup`

<details><summary>Interface Code</summary>

```ts
export interface ErrorGroup {
  group: string;
  items: ErrorItem[];
  uri?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `group` | `string` | ✗ |  |
| `items` | `ErrorItem[]` | ✗ |  |
| `uri` | `string` | ✓ |  |


---

## Type Aliases

### `CompilerFlags`

```ts
type CompilerFlags = Record<string, unknown>;
```

### `SourceType`

```ts
type SourceType = TSESLint.SourceType;
```

### `RulesRecord`

```ts
type RulesRecord = TSESLint.Linter.RulesRecord;
```

### `TabType`

```ts
type TabType = 'code' | 'eslintrc' | 'tsconfig';
```

### `ConfigFileType`

```ts
type ConfigFileType = `${ts.Extension}`;
```

### `ConfigShowAst`

```ts
type ConfigShowAst = 'es' | 'scope' | 'ts' | 'types' | false;
```

### `SelectedRange`

```ts
type SelectedRange = [number, number];
```

### `EslintRC`

```ts
type EslintRC = { rules: RulesRecord } & Record<string, unknown>;
```

### `TSConfig`

```ts
type TSConfig = {
  compilerOptions: CompilerFlags;
} & Record<string, unknown>;
```


---