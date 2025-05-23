[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `RuleAttributes.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 4
- **Classes**: 0
- **Imports**: 14
- **Interfaces**: 0
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/RuleAttributes.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ESLintPluginDocs` | `@typescript-eslint/eslint-plugin/use-at-your-own-risk/rules` |
| `RuleRecommendation` | `@typescript-eslint/utils/ts-eslint` |
| `RuleRecommendationAcrossConfigs` | `@typescript-eslint/utils/ts-eslint` |
| `Link` | `@docusaurus/Link` |
| `useRulesMeta` | `@site/src/hooks/useRulesMeta` |
| `React` | `react` |
| `FeatureProps` | `./Feature` |
| `FIXABLE_EMOJI` | `../../components/constants` |
| `RECOMMENDED_CONFIG_EMOJI` | `../../components/constants` |
| `STRICT_CONFIG_EMOJI` | `../../components/constants` |
| `STYLISTIC_CONFIG_EMOJI` | `../../components/constants` |
| `SUGGESTIONS_EMOJI` | `../../components/constants` |
| `Feature` | `./Feature` |
| `styles` | `./RuleAttributes.module.css` |


---

## Functions

### `isRecommendedDocs(docs: ESLintPluginDocs): docs is RecommendedRuleMetaDataDocs`

<details><summary>Code</summary>

```ts
(
  docs: ESLintPluginDocs,
): docs is RecommendedRuleMetaDataDocs => !!docs.recommended
```
</details>

- **Parameters**:
  - `docs: ESLintPluginDocs`
- **Return Type**: `docs is RecommendedRuleMetaDataDocs`
### `resolveRecommendation(recommended: RuleRecommendationAcrossConfigs<unknown[]>): RuleRecommendation`

<details><summary>Code</summary>

```ts
(
  recommended: RuleRecommendationAcrossConfigs<unknown[]>,
): RuleRecommendation => {
  return recommended.recommended === true ? 'recommended' : 'strict';
}
```
</details>

- **Parameters**:
  - `recommended: RuleRecommendationAcrossConfigs<unknown[]>`
- **Return Type**: `RuleRecommendation`
### `getRecommendation(docs: RecommendedRuleMetaDataDocs): string[]`

<details><summary>Code</summary>

```ts
(docs: RecommendedRuleMetaDataDocs): string[] => {
  const recommended = docs.recommended;
  const recommendation =
    recommendations[
      typeof recommended === 'object'
        ? resolveRecommendation(recommended)
        : recommended
    ];

  return docs.requiresTypeChecking
    ? [recommendation[0], `${recommendation[1]}-type-checked`]
    : recommendation;
}
```
</details>

- **Parameters**:
  - `docs: RecommendedRuleMetaDataDocs`
- **Return Type**: `string[]`
- **Calls**:
  - `resolveRecommendation`
### `RuleAttributes({ name }: { name: string }): React.ReactNode`

<details><summary>Code</summary>

```ts
export function RuleAttributes({ name }: { name: string }): React.ReactNode {
  const rules = useRulesMeta();
  const rule = rules.find(rule => rule.name === name);
  if (!rule?.docs) {
    return null;
  }

  const features: FeatureProps[] = [];

  if (isRecommendedDocs(rule.docs)) {
    const [emoji, recommendation] = getRecommendation(rule.docs);
    features.push({
      children: (
        <>
          Extending{' '}
          <Link to={`/users/configs#${recommendation}`} target="_blank">
            <code className={styles.code}>
              "plugin:@typescript-eslint/{recommendation}"
            </code>
          </Link>{' '}
          in an{' '}
          <Link href="https://eslint.org/docs/latest/user-guide/configuring/configuration-files#extending-configuration-files">
            ESLint configuration
          </Link>{' '}
          enables this rule.
        </>
      ),
      emoji,
    });
  }

  if (rule.fixable) {
    features.push({
      children: (
        <>
          Some problems reported by this rule are automatically fixable by the{' '}
          <Link href="https://eslint.org/docs/latest/user-guide/command-line-interface#--fix">
            <code>--fix</code> ESLint command line option
          </Link>
          .
        </>
      ),
      emoji: FIXABLE_EMOJI,
    });
  }

  if (rule.hasSuggestions) {
    features.push({
      children: (
        <>
          Some problems reported by this rule are manually fixable by editor{' '}
          <Link href="https://eslint.org/docs/latest/developer-guide/working-with-rules#providing-suggestions">
            suggestions
          </Link>
          .
        </>
      ),
      emoji: SUGGESTIONS_EMOJI,
    });
  }

  if (rule.docs.requiresTypeChecking) {
    features.push({
      children: (
        <>
          This rule requires{' '}
          <Link href="/getting-started/typed-linting" target="_blank">
            type information
          </Link>{' '}
          to run, which comes with performance tradeoffs.
        </>
      ),
      emoji: '💭',
    });
  }

  if (rule.docs.extendsBaseRule) {
    features.push({
      children: (
        <>
          {' '}
          This is an "extension" rule that replaces a core ESLint rule to work
          with TypeScript. See{' '}
          <Link href="/rules#extension-rules">Rules &gt; Extension Rules</Link>.
        </>
      ),
      emoji: '🧱',
    });
  }

  return (
    <div className={styles.features}>
      {features.map(feature => (
        <Feature {...feature} key={feature.emoji} />
      ))}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{ name }: { name: string }`
- **Return Type**: `React.ReactNode`
- **Calls**:
  - `useRulesMeta (from @site/src/hooks/useRulesMeta)`
  - `rules.find`
  - `isRecommendedDocs`
  - `getRecommendation`
  - `features.push`
  - `features.map`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MakeRequired<Base, Key extends keyof Base extends keyof Base>`

```ts
type MakeRequired<Base, Key extends keyof Base extends keyof Base> = Omit<Base, Key> &
  Required<Record<Key, NonNullable<Base[Key]>>>;
```

### `RecommendedRuleMetaDataDocs`

```ts
type RecommendedRuleMetaDataDocs = MakeRequired<
  ESLintPluginDocs,
  'recommended'
>;
```


---