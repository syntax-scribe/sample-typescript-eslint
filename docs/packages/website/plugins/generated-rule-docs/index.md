[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 18 |
| 📊 Variables & Constants | 3 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 1 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Async/Await Patterns](#asyncawait-patterns)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/plugins/generated-rule-docs/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleModuleWithMetaDocs` | `@typescript-eslint/utils/ts-eslint` |
| `Plugin` | `unified` |
| `pluginRules` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `fromMarkdown` | `mdast-util-from-markdown` |
| `RuleDocsPage` | `./RuleDocsPage` |
| `nodeIsParagraph` | `../utils/nodes` |
| `nodeIsParent` | `../utils/nodes` |
| `isESLintPluginRuleModule` | `../utils/rules` |
| `isVFileWithStem` | `../utils/rules` |
| `addESLintHashToCodeBlocksMeta` | `./addESLintHashToCodeBlocksMeta` |
| `createRuleDocsPage` | `./createRuleDocsPage` |
| `insertBaseRuleReferences` | `./insertions/insertBaseRuleReferences` |
| `insertNewRuleReferences` | `./insertions/insertNewRuleReferences` |
| `insertResources` | `./insertions/insertResources` |
| `insertRuleDescription` | `./insertions/insertRuleDescription` |
| `insertRuleOptions` | `./insertions/insertRuleOptions` |
| `insertWhenNotToUseIt` | `./insertions/insertWhenNotToUseIt` |
| `removeSourceCodeNotice` | `./removeSourceCodeNotice` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `rule` | `any` | let/var | `pluginRules[file.stem]` | ✗ |
| `eslintrc` | `string` | let/var | `rule.meta.docs.extendsBaseRule
      ? insertBaseRuleReferences(page)
      : await insertNewRuleReferences(page)` | ✗ |
| `baseRule` | `any` | const | `typeof rule.meta.docs.extendsBaseRule === 'string'
      ? rule.meta.docs.extendsBaseRule
      : stem` | ✗ |


---

## Async/Await Patterns

| Type | Function | Await Expressions | Promise Chains |
|------|----------|-------------------|----------------|
| await-expression | `generatedRuleDocs` | insertNewRuleReferences(page) | *none* |


---

## Functions

### `generatedRuleDocs(): (root: any, file: any) => Promise<void>`

<details><summary>Code</summary>

```ts
() => {
  return async (root, file) => {
    if (!nodeIsParent(root) || !isVFileWithStem(file)) {
      return;
    }

    const rule = pluginRules[file.stem];
    if (!isESLintPluginRuleModule(rule)) {
      return;
    }

    const page = createRuleDocsPage(root.children, file, rule);

    removeSourceCodeNotice(page);
    insertRuleDescription(page);

    const eslintrc = rule.meta.docs.extendsBaseRule
      ? insertBaseRuleReferences(page)
      : await insertNewRuleReferences(page);

    insertWhenNotToUseIt(page);
    insertResources(page);
    insertRuleOptions(page);
    addESLintHashToCodeBlocksMeta(page, eslintrc);
    insertExtensionNotice(page, rule, file.stem);
  };
}
```
</details>

- **Return Type**: `(root: any, file: any) => Promise<void>`
- **Calls**:
  - `nodeIsParent (from ../utils/nodes)`
  - `isVFileWithStem (from ../utils/rules)`
  - `isESLintPluginRuleModule (from ../utils/rules)`
  - `createRuleDocsPage (from ./createRuleDocsPage)`
  - `removeSourceCodeNotice (from ./removeSourceCodeNotice)`
  - `insertRuleDescription (from ./insertions/insertRuleDescription)`
  - `insertBaseRuleReferences (from ./insertions/insertBaseRuleReferences)`
  - `insertNewRuleReferences (from ./insertions/insertNewRuleReferences)`
  - `insertWhenNotToUseIt (from ./insertions/insertWhenNotToUseIt)`
  - `insertResources (from ./insertions/insertResources)`
  - `insertRuleOptions (from ./insertions/insertRuleOptions)`
  - `addESLintHashToCodeBlocksMeta (from ./addESLintHashToCodeBlocksMeta)`
  - `insertExtensionNotice`
### `insertExtensionNotice(page: RuleDocsPage, rule: RuleModuleWithMetaDocs<string, unknown[], pluginRules.ESLintPluginDocs>, stem: string): void`

<details><summary>Code</summary>

```ts
function insertExtensionNotice(
  page: RuleDocsPage,
  rule: RuleModuleWithMetaDocs<string, unknown[], pluginRules.ESLintPluginDocs>,
  stem: string,
) {
  if (!rule.meta.docs.extendsBaseRule) {
    return;
  }

  const baseRule =
    typeof rule.meta.docs.extendsBaseRule === 'string'
      ? rule.meta.docs.extendsBaseRule
      : stem;

  const firstParagraph = page.children.find(nodeIsParagraph);

  if (!firstParagraph) {
    if (rule.meta.deprecated) {
      return;
    }

    throw new Error(`Missing first paragraph for extension rule ${stem}.`);
  }

  const addition = fromMarkdown(
    `This rule extends the base [\`${baseRule}\`](https://eslint.org/docs/latest/rules/${baseRule}) rule from ESLint core.`,
  );

  firstParagraph.children.unshift(
    ...(addition.children[0] as mdast.Paragraph).children,
    {
      type: 'text',
      value: ' ',
    },
  );
}
```
</details>

- **Parameters**:
  - `page: RuleDocsPage`
  - `rule: RuleModuleWithMetaDocs<string, unknown[], pluginRules.ESLintPluginDocs>`
  - `stem: string`
- **Return Type**: `void`
- **Calls**:
  - `page.children.find`
  - `fromMarkdown (from mdast-util-from-markdown)`
  - `firstParagraph.children.unshift`

---