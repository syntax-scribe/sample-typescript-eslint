[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `addESLintHashToCodeBlocksMeta.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 4 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/addESLintHashToCodeBlocksMeta.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `MdxJsxFlowElement` | `mdast-util-mdx` |
| `RuleDocsPage` | `./RuleDocsPage` |
| `nodeIsCode` | `../utils/nodes` |
| `convertToPlaygroundHash` | `../utils/rules` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `optionRegex` | `RegExp` | const | `/option='(?<option>.*?)'/` | ✗ |
| `playgroundEslintrc` | `string` | let/var | `eslintrc` | ✗ |
| `option` | `any` | const | `node.meta?.match(optionRegex)?.groups?.option` | ✗ |


---

## Functions

### `nodeIsJsxTabs(node: unist.Node): node is MdxJsxFlowElement`

<details><summary>Code</summary>

```ts
function nodeIsJsxTabs(node: unist.Node): node is MdxJsxFlowElement {
  return (
    node.type === 'mdxJsxFlowElement' && 'name' in node && node.name === 'Tabs'
  );
}
```
</details>

- **Parameters**:
  - `node: unist.Node`
- **Return Type**: `node is MdxJsxFlowElement`
### `addESLintHashToCodeBlocksMeta(page: RuleDocsPage, eslintrc: string): void`

<details><summary>Code</summary>

```ts
export function addESLintHashToCodeBlocksMeta(
  page: RuleDocsPage,
  eslintrc: string,
): void {
  for (const node of page.children) {
    if (nodeIsJsxTabs(node)) {
      addHashesToChildrenTabs(node);
    } else {
      addHashToNodeIfCode(node);
    }
  }

  function addHashesToChildrenTabs(node: MdxJsxFlowElement): void {
    for (const tabItem of node.children) {
      if ('children' in tabItem) {
        for (const child of tabItem.children) {
          addHashToNodeIfCode(child, true);
        }
      }
    }
  }

  function addHashToNodeIfCode(node: unist.Node, insideTab?: boolean): void {
    if (
      nodeIsCode(node) &&
      (insideTab || node.meta?.includes('showPlaygroundButton')) &&
      !node.meta?.includes('title="eslint.config.mjs"') &&
      !node.meta?.includes('title=".eslintrc.cjs"') &&
      !node.meta?.includes('eslintrcHash=')
    ) {
      let playgroundEslintrc = eslintrc;
      const option = node.meta?.match(optionRegex)?.groups?.option;
      if (option) {
        playgroundEslintrc = playgroundEslintrc.replace(
          '"error"',
          `["error", ${option}]`,
        );
        try {
          playgroundEslintrc = JSON.stringify(
            JSON.parse(playgroundEslintrc),
            null,
            2,
          );
        } catch (err) {
          // eslint-disable-next-line no-console
          console.error(
            `Invalid JSON detected in ${page.file.basename}. Check the \`option\` in the meta strings of code blocks.`,
          );
          throw err;
        }
      }

      node.meta = [
        node.meta,
        `eslintrcHash="${convertToPlaygroundHash(playgroundEslintrc)}"`,
      ]
        .filter(Boolean)
        .join(' ');
    }
  }
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
  - `eslintrc: string`
- **Return Type**: `void`
- **Calls**:
  - `nodeIsJsxTabs`
  - `addHashesToChildrenTabs`
  - `addHashToNodeIfCode`
  - `nodeIsCode (from ../utils/nodes)`
  - `node.meta?.includes`
  - `node.meta?.match`
  - `playgroundEslintrc.replace`
  - `JSON.stringify`
  - `JSON.parse`
  - `console.error`
  - `[
        node.meta,
        `eslintrcHash="${convertToPlaygroundHash(playgroundEslintrc)}"`,
      ]
        .filter(Boolean)
        .join`
- **Internal Comments**:
```
// eslint-disable-next-line no-console (x4)
```

### `addHashesToChildrenTabs(node: MdxJsxFlowElement): void`

<details><summary>Code</summary>

```ts
function addHashesToChildrenTabs(node: MdxJsxFlowElement): void {
    for (const tabItem of node.children) {
      if ('children' in tabItem) {
        for (const child of tabItem.children) {
          addHashToNodeIfCode(child, true);
        }
      }
    }
  }
```
</details>

- **Parameters**:
  - `node: MdxJsxFlowElement`
- **Return Type**: `void`
- **Calls**:
  - `addHashToNodeIfCode`
### `addHashToNodeIfCode(node: unist.Node, insideTab: boolean): void`

<details><summary>Code</summary>

```ts
function addHashToNodeIfCode(node: unist.Node, insideTab?: boolean): void {
    if (
      nodeIsCode(node) &&
      (insideTab || node.meta?.includes('showPlaygroundButton')) &&
      !node.meta?.includes('title="eslint.config.mjs"') &&
      !node.meta?.includes('title=".eslintrc.cjs"') &&
      !node.meta?.includes('eslintrcHash=')
    ) {
      let playgroundEslintrc = eslintrc;
      const option = node.meta?.match(optionRegex)?.groups?.option;
      if (option) {
        playgroundEslintrc = playgroundEslintrc.replace(
          '"error"',
          `["error", ${option}]`,
        );
        try {
          playgroundEslintrc = JSON.stringify(
            JSON.parse(playgroundEslintrc),
            null,
            2,
          );
        } catch (err) {
          // eslint-disable-next-line no-console
          console.error(
            `Invalid JSON detected in ${page.file.basename}. Check the \`option\` in the meta strings of code blocks.`,
          );
          throw err;
        }
      }

      node.meta = [
        node.meta,
        `eslintrcHash="${convertToPlaygroundHash(playgroundEslintrc)}"`,
      ]
        .filter(Boolean)
        .join(' ');
    }
  }
```
</details>

- **Parameters**:
  - `node: unist.Node`
  - `insideTab: boolean`
- **Return Type**: `void`
- **Calls**:
  - `nodeIsCode (from ../utils/nodes)`
  - `node.meta?.includes`
  - `node.meta?.match`
  - `playgroundEslintrc.replace`
  - `JSON.stringify`
  - `JSON.parse`
  - `console.error`
  - `[
        node.meta,
        `eslintrcHash="${convertToPlaygroundHash(playgroundEslintrc)}"`,
      ]
        .filter(Boolean)
        .join`
- **Internal Comments**:
```
// eslint-disable-next-line no-console (x4)
```


---