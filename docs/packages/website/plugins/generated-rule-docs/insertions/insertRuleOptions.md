[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `insertRuleOptions.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 3
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/insertions/insertRuleOptions.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `JSONSchema4` | `@typescript-eslint/utils/json-schema` |
| `Node` | `unist` |
| `RuleDocsPage` | `../RuleDocsPage` |
| `nodeIsHeading` | `../../utils/nodes` |
| `nodeIsMdxFlowExpression` | `../../utils/nodes` |
| `findHeadingIndex` | `../../utils/rules` |


---

## Functions

### `insertRuleOptions(page: RuleDocsPage): void`

<details><summary>Code</summary>

```ts
export function insertRuleOptions(page: RuleDocsPage): void {
  if (
    knownSkippedRules.has(page.file.stem) ||
    !Array.isArray(page.rule.meta.schema)
  ) {
    return;
  }

  const optionProperties = getOptionProperties(
    (page.rule.meta.schema as JSONSchema4[]).at(0),
  );

  if (!optionProperties) {
    return;
  }

  const defaultOptions = (page.rule.defaultOptions[0] ?? {}) as Record<
    string,
    unknown
  >;

  for (const [optionName, option] of Object.entries(optionProperties)) {
    if (!option.description) {
      if (!page.rule.meta.docs.extendsBaseRule) {
        throw new Error(`Missing description for option ${optionName}.`);
      }
      return;
    }

    const existingHeadingIndex = findHeadingIndex(
      page.children,
      3,
      node => node.type === 'inlineCode' && node.value === optionName,
    );
    if (existingHeadingIndex === -1) {
      if (!page.rule.meta.docs.extendsBaseRule) {
        throw new Error(`Couldn't find h3 for option ${optionName}.`);
      }
      continue;
    }

    const commentInsertionIndex = findCommentIndexForOption(
      page.children,
      existingHeadingIndex,
    );
    if (commentInsertionIndex === -1) {
      throw new Error(
        `[${page.file.stem}] Could not find ${OPTION_COMMENT} under option heading ${optionName}.`,
      );
    }

    const defaultValue =
      defaultOptions[optionName] ?? emptyOptionDefaults.get(option.type);

    page.spliceChildren(
      commentInsertionIndex,
      0,
      // eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- I don't know whether this is safe to fix
      defaultValue !== undefined
        ? `${option.description} Default: \`${JSON.stringify(defaultValue)}\`.`
        : option.description,
    );
  }
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
- **Return Type**: `void`
- **Calls**:
  - `knownSkippedRules.has`
  - `Array.isArray`
  - `getOptionProperties`
  - `(page.rule.meta.schema as JSONSchema4[]).at`
  - `Object.entries`
  - `findHeadingIndex (from ../../utils/rules)`
  - `findCommentIndexForOption`
  - `emptyOptionDefaults.get`
  - `page.spliceChildren`
  - `JSON.stringify`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/eqeq-nullish -- I don't know whether this is safe to fix (x3)
```

### `findCommentIndexForOption(children: readonly Node[], headingIndex: number): number`

<details><summary>Code</summary>

```ts
function findCommentIndexForOption(
  children: readonly Node[],
  headingIndex: number,
): number {
  for (let i = headingIndex + 1; i < children.length; i += 1) {
    const child = children[i];
    if (nodeIsMdxFlowExpression(child) && child.value === OPTION_COMMENT) {
      return i;
    }

    if (nodeIsHeading(child)) {
      break;
    }
  }

  return -1;
}
```
</details>

- **Parameters**:
  - `children: readonly Node[]`
  - `headingIndex: number`
- **Return Type**: `number`
- **Calls**:
  - `nodeIsMdxFlowExpression (from ../../utils/nodes)`
  - `nodeIsHeading (from ../../utils/nodes)`
### `getOptionProperties(options: JSONSchema4 | undefined): Record<string, JSONSchema4> | undefined`

<details><summary>Code</summary>

```ts
function getOptionProperties(
  options: JSONSchema4 | undefined,
): Record<string, JSONSchema4> | undefined {
  if (!options) {
    return undefined;
  }

  if (options.type === 'object') {
    return options.properties;
  }

  if (options.oneOf) {
    return options.oneOf.reduce<Record<string, JSONSchema4>>(
      (previous, next) => ({
        ...previous,
        ...getOptionProperties(next),
      }),
      {},
    );
  }

  return undefined;
}
```
</details>

- **Parameters**:
  - `options: JSONSchema4 | undefined`
- **Return Type**: `Record<string, JSONSchema4> | undefined`
- **Calls**:
  - `options.oneOf.reduce`
  - `getOptionProperties`

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