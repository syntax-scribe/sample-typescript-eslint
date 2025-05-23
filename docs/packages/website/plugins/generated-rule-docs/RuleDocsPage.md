[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `RuleDocsPage.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 1
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/RuleDocsPage.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintPluginRuleModule` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `fromMarkdown` | `mdast-util-from-markdown` |
| `VFileWithStem` | `../utils/rules` |
| `findHeadingIndex` | `../utils/rules` |


---

## Functions

### `RuleDocsPage.#recreateHeadingIndices(): RequiredHeadingIndices`

<details><summary>Code</summary>

```ts
#recreateHeadingIndices(): RequiredHeadingIndices {
    return {
      howToUse: findHeadingIndex(this.#children, 2, requiredHeadingNames[0]),
      options: findHeadingIndex(this.#children, 2, requiredHeadingNames[1]),
      whenNotToUseIt: findHeadingIndex(
        this.#children,
        2,
        requiredHeadingNames[2],
      ),
    };
  }
```
</details>

- **Return Type**: `RequiredHeadingIndices`
- **Calls**:
  - `findHeadingIndex (from ../utils/rules)`
### `RuleDocsPage.spliceChildren(start: number, deleteCount: number, items: (string | unist.Node)[]): void`

<details><summary>Code</summary>

```ts
spliceChildren(
    start: number,
    deleteCount: number,
    ...items: (string | unist.Node)[]
  ): void {
    this.#children.splice(
      start,
      deleteCount,
      ...items.map(item =>
        typeof item === 'string' ? fromMarkdown(item) : item,
      ),
    );
    this.#headingIndices = this.#recreateHeadingIndices();
  }
```
</details>

- **Parameters**:
  - `start: number`
  - `deleteCount: number`
  - `items: (string | unist.Node)[]`
- **Return Type**: `void`
- **Calls**:
  - `this.#children.splice`
  - `items.map`
  - `fromMarkdown (from mdast-util-from-markdown)`
  - `this.#recreateHeadingIndices`

---

## Classes

### `RuleDocsPage`

<details><summary>Class Code</summary>

```ts
export class RuleDocsPage {
  #children: unist.Node[];
  #file: Readonly<VFileWithStem>;
  #headingIndices: RequiredHeadingIndices;
  #rule: Readonly<ESLintPluginRuleModule>;

  constructor(
    children: unist.Node[],
    file: Readonly<VFileWithStem>,
    rule: Readonly<ESLintPluginRuleModule>,
  ) {
    this.#children = children;
    this.#file = file;
    this.#headingIndices = this.#recreateHeadingIndices();
    this.#rule = rule;
  }

  #recreateHeadingIndices(): RequiredHeadingIndices {
    return {
      howToUse: findHeadingIndex(this.#children, 2, requiredHeadingNames[0]),
      options: findHeadingIndex(this.#children, 2, requiredHeadingNames[1]),
      whenNotToUseIt: findHeadingIndex(
        this.#children,
        2,
        requiredHeadingNames[2],
      ),
    };
  }

  spliceChildren(
    start: number,
    deleteCount: number,
    ...items: (string | unist.Node)[]
  ): void {
    this.#children.splice(
      start,
      deleteCount,
      ...items.map(item =>
        typeof item === 'string' ? fromMarkdown(item) : item,
      ),
    );
    this.#headingIndices = this.#recreateHeadingIndices();
  }

  get children(): readonly unist.Node[] {
    return this.#children;
  }

  get file(): Readonly<VFileWithStem> {
    return this.#file;
  }

  get headingIndices(): Readonly<RequiredHeadingIndices> {
    return this.#headingIndices;
  }

  get rule(): Readonly<ESLintPluginRuleModule> {
    return this.#rule;
  }
}
```
</details>

#### Methods

##### `#recreateHeadingIndices(): RequiredHeadingIndices`

<details><summary>Code</summary>

```ts
#recreateHeadingIndices(): RequiredHeadingIndices {
    return {
      howToUse: findHeadingIndex(this.#children, 2, requiredHeadingNames[0]),
      options: findHeadingIndex(this.#children, 2, requiredHeadingNames[1]),
      whenNotToUseIt: findHeadingIndex(
        this.#children,
        2,
        requiredHeadingNames[2],
      ),
    };
  }
```
</details>

##### `spliceChildren(start: number, deleteCount: number, items: (string | unist.Node)[]): void`

<details><summary>Code</summary>

```ts
spliceChildren(
    start: number,
    deleteCount: number,
    ...items: (string | unist.Node)[]
  ): void {
    this.#children.splice(
      start,
      deleteCount,
      ...items.map(item =>
        typeof item === 'string' ? fromMarkdown(item) : item,
      ),
    );
    this.#headingIndices = this.#recreateHeadingIndices();
  }
```
</details>


---

## Interfaces

### `RequiredHeadingIndices`

<details><summary>Interface Code</summary>

```ts
export interface RequiredHeadingIndices {
  howToUse: number;
  options: number;
  whenNotToUseIt: number;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `howToUse` | `number` | ✗ |  |
| `options` | `number` | ✗ |  |
| `whenNotToUseIt` | `number` | ✗ |  |


---

## Type Aliases

### `HeadingName`

```ts
type HeadingName = (typeof requiredHeadingNames)[number];
```


---