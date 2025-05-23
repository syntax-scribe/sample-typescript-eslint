[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Processor.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 3
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/utils/src/ts-eslint/Processor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Linter` | `./Linter` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ProcessorMeta`

<details><summary>Interface Code</summary>

```ts
export interface ProcessorMeta {
    /**
     * The unique name of the processor.
     */
    name: string;
    /**
     * The a string identifying the version of the processor.
     */
    version?: string;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `name` | `string` | ✗ |  |
| `version` | `string` | ✓ |  |

### `ProcessorModule`

<details><summary>Interface Code</summary>

```ts
export interface ProcessorModule {
    /**
     * Information about the processor to uniquely identify it when serializing.
     */
    meta?: ProcessorMeta;

    /**
     * The function to merge messages.
     */
    postprocess?: PostProcess;

    /**
     * The function to extract code blocks.
     */
    preprocess?: PreProcess;

    /**
     * If `true` then it means the processor supports autofix.
     */
    supportsAutofix?: boolean;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `meta` | `ProcessorMeta` | ✓ |  |
| `postprocess` | `PostProcess` | ✓ |  |
| `preprocess` | `PreProcess` | ✓ |  |
| `supportsAutofix` | `boolean` | ✓ |  |

### `LooseProcessorModule`

<details><summary>Interface Code</summary>

```ts
export interface LooseProcessorModule {
    /**
     * Information about the processor to uniquely identify it when serializing.
     */
    meta?: { [K in keyof ProcessorMeta]?: ProcessorMeta[K] | undefined };

    /**
     * The function to merge messages.
     */
    /*
    eslint-disable-next-line @typescript-eslint/no-explicit-any --
    intentionally using `any` to allow bi-directional assignment (unknown and
    never only allow unidirectional)
    */
    postprocess?: (messagesList: any, filename: string) => any;

    /**
     * The function to extract code blocks.
     */
    /*
    eslint-disable-next-line @typescript-eslint/no-explicit-any --
    intentionally using `any` to allow bi-directional assignment (unknown and
    never only allow unidirectional)
    */
    preprocess?: (text: string, filename: string) => any;

    /**
     * If `true` then it means the processor supports autofix.
     */
    supportsAutofix?: boolean | undefined;
  }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `meta` | `{ [K in keyof ProcessorMeta]?: ProcessorMeta[K] | undefined }` | ✓ |  |
| `postprocess` | `(messagesList: any, filename: string) => any` | ✓ |  |
| `preprocess` | `(text: string, filename: string) => any` | ✓ |  |
| `supportsAutofix` | `boolean | undefined` | ✓ |  |


---

## Type Aliases

### `PreProcess`

```ts
type PreProcess = (
    text: string,
    filename: string,
  ) => (string | { filename: string; text: string })[];
```

### `PostProcess`

```ts
type PostProcess = (
    messagesList: Linter.LintMessage[][],
    filename: string,
  ) => Linter.LintMessage[];
```


---