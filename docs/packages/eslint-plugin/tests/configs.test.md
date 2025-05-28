[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `configs.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 4 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/configs.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleRecommendation` | `@typescript-eslint/utils/ts-eslint` |
| `plugin` | `../src/index.js` |
| `rules` | `../src/rules/index.js` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `RULE_NAME_PREFIX` | `"@typescript-eslint/"` | const | `'@typescript-eslint/'` | ✗ |
| `result` | `[string, unknown][]` | let/var | `rulesEntriesList` | ✗ |
| `customRecommendation` | `any` | const | `highestRecommendation &&
      typeof rule.meta.docs?.recommended === 'object' &&
      rule.meta.docs.recommended[
        highestRecommendation as 'recommended' | 'strict'
      ]` | ✗ |
| `ruleNames` | `Set<string>` | let/var | `new Set(Object.keys(unfilteredConfigRules))` | ✗ |


---

## Functions

### `filterRules(values: Record<string, string | unknown[]>): [string, string | unknown[]][]`

<details><summary>Code</summary>

```ts
function filterRules(
  values: Record<string, string | unknown[]>,
): [string, string | unknown[]][] {
  return Object.entries(values).filter(([name]) =>
    name.startsWith(RULE_NAME_PREFIX),
  );
}
```
</details>

- **Parameters**:
  - `values: Record<string, string | unknown[]>`
- **Return Type**: `[string, string | unknown[]][]`
- **Calls**:
  - `Object.entries(values).filter`
  - `name.startsWith`
### `filterAndMapRuleConfigs({
  excludeDeprecated,
  recommendations,
  typeChecked,
}: FilterAndMapRuleConfigsSettings): [string, unknown][]`

<details><summary>Code</summary>

```ts
function filterAndMapRuleConfigs({
  excludeDeprecated,
  recommendations,
  typeChecked,
}: FilterAndMapRuleConfigsSettings = {}): [string, unknown][] {
  let result = rulesEntriesList;

  if (excludeDeprecated) {
    result = result.filter(([, rule]) => !rule.meta.deprecated);
  }

  if (typeChecked) {
    result = result.filter(([, rule]) =>
      typeChecked === 'exclude'
        ? !rule.meta.docs?.requiresTypeChecking
        : rule.meta.docs?.requiresTypeChecking,
    );
  }

  if (recommendations) {
    result = result.filter(([, rule]) => {
      switch (typeof rule.meta.docs?.recommended) {
        case 'object':
          return Object.keys(rule.meta.docs.recommended).some(recommended =>
            recommendations.includes(recommended as RuleRecommendation),
          );
        case 'string':
          return recommendations.includes(rule.meta.docs.recommended);
        default:
          return false;
      }
    });
  }

  const highestRecommendation = recommendations?.filter(Boolean).at(-1);

  return result.map(([name, rule]) => {
    const customRecommendation =
      highestRecommendation &&
      typeof rule.meta.docs?.recommended === 'object' &&
      rule.meta.docs.recommended[
        highestRecommendation as 'recommended' | 'strict'
      ];

    return [
      `${RULE_NAME_PREFIX}${name}`,
      customRecommendation && typeof customRecommendation !== 'boolean'
        ? ['error', customRecommendation[0]]
        : 'error',
    ];
  });
}
```
</details>

- **Parameters**:
  - `{
  excludeDeprecated,
  recommendations,
  typeChecked,
}: FilterAndMapRuleConfigsSettings`
- **Return Type**: `[string, unknown][]`
- **Calls**:
  - `result.filter`
  - `Object.keys(rule.meta.docs.recommended).some`
  - `recommendations.includes`
  - `recommendations?.filter(Boolean).at`
  - `result.map`

---

## Interfaces

### `FilterAndMapRuleConfigsSettings`

<details><summary>Interface Code</summary>

```ts
interface FilterAndMapRuleConfigsSettings {
  excludeDeprecated?: boolean;
  recommendations?: (RuleRecommendation | undefined)[];
  typeChecked?: 'exclude' | 'include-only';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `excludeDeprecated` | `boolean` | ✓ |  |
| `recommendations` | `(RuleRecommendation | undefined)[]` | ✓ |  |
| `typeChecked` | `'exclude' | 'include-only'` | ✓ |  |


---