[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertWhenNotToUseIt.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertWhenNotToUseIt.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleDocsPage` | `../RuleDocsPage` |
| `nodeIsHeading` | `../../utils/nodes` |


---

## Functions

### `insertWhenNotToUseIt(page: RuleDocsPage): void`

<details><summary>Code</summary>

```ts
export function insertWhenNotToUseIt(page: RuleDocsPage): void {
  if (!page.rule.meta.docs.requiresTypeChecking) {
    return;
  }

  const hasExistingText =
    page.headingIndices.whenNotToUseIt < page.children.length - 1 &&
    page.children[page.headingIndices.whenNotToUseIt + 1].type !== 'heading';

  const nextHeadingIndex =
    page.children.findIndex(
      child => nodeIsHeading(child) && child.depth === 2,
      page.headingIndices.whenNotToUseIt + 1,
    ) +
    page.headingIndices.whenNotToUseIt +
    1;

  page.spliceChildren(
    nextHeadingIndex === -1 ? page.children.length : nextHeadingIndex - 1,
    0,
    ...(hasExistingText ? ['---'] : []),
    'Type checked lint rules are more powerful than traditional lint rules, but also require configuring [type checked linting](/getting-started/typed-linting).',
    'See [Troubleshooting > Linting with Type Information > Performance](/troubleshooting/typed-linting/performance) if you experience performance degradations after enabling type checked rules.',
  );
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `void`
- **Calls**:
  - `page.children.findIndex`
  - `nodeIsHeading (from ../../utils/nodes)`
  - `page.spliceChildren`

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