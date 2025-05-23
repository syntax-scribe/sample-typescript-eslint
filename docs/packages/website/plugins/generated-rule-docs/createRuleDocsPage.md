[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `createRuleDocsPage.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/createRuleDocsPage.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintPluginRuleModule` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `VFileWithStem` | `../utils/rules` |
| `HeadingName` | `./RuleDocsPage` |
| `findHeadingIndex` | `../utils/rules` |
| `requiredHeadingNames` | `./RuleDocsPage` |
| `RuleDocsPage` | `./RuleDocsPage` |


---

## Functions

### `createRuleDocsPage(children: unist.Node[], file: Readonly<VFileWithStem>, rule: Readonly<ESLintPluginRuleModule>): RuleDocsPage`

<details><summary>Code</summary>

```ts
export function createRuleDocsPage(
  children: unist.Node[],
  file: Readonly<VFileWithStem>,
  rule: Readonly<ESLintPluginRuleModule>,
): RuleDocsPage {
  const headingIndices = requiredHeadingNames.map(headingName =>
    findHeadingIndex(children, 2, headingName),
  );

  function insertIfMissing(
    headingName: HeadingName,
    insertionIndex?: number,
  ): void {
    if (headingIndices[requiredHeadingNames.indexOf(headingName)] !== -1) {
      return;
    }

    // Unless otherwise specified: if the heading doesn't yet exist,
    // insert it before the first heading that does,
    // or if none yet exist, push it to the end of children.
    insertionIndex ??=
      headingIndices.find(existingIndex => existingIndex !== -1) ??
      children.length;

    children.splice(insertionIndex, 0, {
      children: [
        {
          type: 'text',
          value: headingName,
        },
      ],
      depth: 2,
      type: 'heading',
    } as mdast.Heading);
  }

  insertIfMissing('Options');

  if (rule.meta.docs.extendsBaseRule) {
    insertIfMissing('How to Use');
  }

  if (rule.meta.docs.requiresTypeChecking) {
    insertIfMissing(
      'When Not To Use It',
      headingIndices[3] === -1 ? children.length : headingIndices[3],
    );
  }

  return new RuleDocsPage(children, file, rule);
}
```
</details>

- **Parameters**:
  - `children: unist.Node[]`
  - `file: Readonly<VFileWithStem>`
  - `rule: Readonly<ESLintPluginRuleModule>`
- **Return Type**: `RuleDocsPage`
- **Calls**:
  - `requiredHeadingNames.map`
  - `findHeadingIndex (from ../utils/rules)`
  - `requiredHeadingNames.indexOf`
  - `headingIndices.find`
  - `children.splice`
  - `insertIfMissing`
- **Internal Comments**:
```
// Unless otherwise specified: if the heading doesn't yet exist, (x3)
// insert it before the first heading that does, (x3)
// or if none yet exist, push it to the end of children. (x3)
```

### `insertIfMissing(headingName: HeadingName, insertionIndex: number): void`

<details><summary>Code</summary>

```ts
function insertIfMissing(
    headingName: HeadingName,
    insertionIndex?: number,
  ): void {
    if (headingIndices[requiredHeadingNames.indexOf(headingName)] !== -1) {
      return;
    }

    // Unless otherwise specified: if the heading doesn't yet exist,
    // insert it before the first heading that does,
    // or if none yet exist, push it to the end of children.
    insertionIndex ??=
      headingIndices.find(existingIndex => existingIndex !== -1) ??
      children.length;

    children.splice(insertionIndex, 0, {
      children: [
        {
          type: 'text',
          value: headingName,
        },
      ],
      depth: 2,
      type: 'heading',
    } as mdast.Heading);
  }
```
</details>

- **Parameters**:
  - `headingName: HeadingName`
  - `insertionIndex: number`
- **Return Type**: `void`
- **Calls**:
  - `requiredHeadingNames.indexOf`
  - `headingIndices.find`
  - `children.splice`
- **Internal Comments**:
```
// Unless otherwise specified: if the heading doesn't yet exist, (x3)
// insert it before the first heading that does, (x3)
// or if none yet exist, push it to the end of children. (x3)
```


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