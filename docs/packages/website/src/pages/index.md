[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 49 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/website/src/pages/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `useBaseUrl` | `@docusaurus/useBaseUrl` |
| `useDocusaurusContext` | `@docusaurus/useDocusaurusContext` |
| `Heading` | `@theme/Heading` |
| `Layout` | `@theme/Layout` |
| `clsx` | `clsx` |
| `React` | `react` |
| `FinancialContributors` | `../components/FinancialContributors` |
| `styles` | `./styles.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `features` | `FeatureItem[]` | const | `[
  {
    description: (
      <>
        <div className="row padding-vert--lg">
          <div className="col col--2 text--center">
            <img
              alt="eslint"
              className={styles.featureImage}
              src="/img/eslint.svg"
            />
          </div>
          <div className="col col--8">
            <h3 className="text--justify">
              <b>ESLint</b> is an awesome linter for JavaScript code.
            </h3>
            <p className="text--justify">
              ESLint statically analyzes your code to quickly find problems. It
              allows creating a series of assertions called lint rules around
              what your code should look or behave like, as well as auto-fixer
              suggestions to improve your code for you, and loading in lint
              rules from shared plugins.
            </p>
          </div>
        </div>
        <div className="row padding-vert--lg">
          <div className="col col--2 text--center">
            <img
              alt="TypeScript"
              className={styles.featureImage}
              src="/img/typescript.svg"
            />
          </div>
          <div className="col col--8">
            <h3 className="text--justify">
              <b>TypeScript</b> is a strongly typed programming language that
              builds on JavaScript.
            </h3>
            <p className="text--justify">
              TypeScript adds additional syntax to JavaScript that allows you to
              declare the shapes of objects and functions in code. It provides a
              set of language services that allow for running powerful
              inferences and automations with that type information.
            </p>
          </div>
        </div>
      </>
    ),
    title: 'What are ESLint and TypeScript, and how do they compare?',
  },
  {
    description: (
      <div className="row padding-vert--lg text--justify">
        <div className="col col--offset-2 col--8">
          <p>
            <strong>
              typescript-eslint enables ESLint to run on TypeScript code.
            </strong>{' '}
            It brings in the best of both tools to help you write the best
            JavaScript or TypeScript code you possibly can.
          </p>
        </div>
        <div className="col col--offset-2 col--8">
          <p>
            ESLint and TypeScript represent code differently internally.
            ESLint's default JavaScript parser cannot natively read in
            TypeScript-specific syntax and its rules don't natively have access
            to TypeScript's type information.
          </p>
        </div>
        <div className="col col--offset-2 col--8">
          typescript-eslint:
          <ul>
            <li>allows ESLint to parse TypeScript syntax</li>
            <li>
              creates a set of tools for ESLint rules to be able to use
              TypeScript's type information
            </li>
            <li>
              provides a large list of lint rules that are specific to
              TypeScript and/or use that type information
            </li>
          </ul>
        </div>
      </div>
    ),
    title: 'Why does this project exist?',
  },
]` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Fragment` | fragment | *none* | <div>, <div> |
| `div` | element | className="row padding-vert--lg" | <div>, <div> |
| `div` | element | className="col col--2 text--center" | <img> |
| `img` | element | alt="eslint", className={styles.featureImage}, src="/img/eslint.svg" | *none* |
| `div` | element | className="col col--8" | <h3>, <p> |
| `h3` | element | className="text--justify" | <b>, text: "is an awesome linter for JavaScript code." |
| `b` | element | *none* | text: "ESLint" |
| `p` | element | className="text--justify" | text: "ESLint statically analyzes your code to quickly find problems. It
              allows creating a series of assertions called lint rules around
              what your code should look or behave like, as well as auto-fixer
              suggestions to improve your code for you, and loading in lint
              rules from shared plugins." |
| `div` | element | className="row padding-vert--lg" | <div>, <div> |
| `div` | element | className="col col--2 text--center" | <img> |
| `img` | element | alt="TypeScript", className={styles.featureImage}, src="/img/typescript.svg" | *none* |
| `div` | element | className="col col--8" | <h3>, <p> |
| `h3` | element | className="text--justify" | <b>, text: "is a strongly typed programming language that
              builds on JavaScript." |
| `b` | element | *none* | text: "TypeScript" |
| `p` | element | className="text--justify" | text: "TypeScript adds additional syntax to JavaScript that allows you to
              declare the shapes of objects and functions in code. It provides a
              set of language services that allow for running powerful
              inferences and automations with that type information." |
| `div` | element | className="row padding-vert--lg text--justify" | <div>, <div>, <div> |
| `div` | element | className="col col--offset-2 col--8" | <p> |
| `p` | element | *none* | <strong>, {' '}, text: "It brings in the best of both tools to help you write the best
            JavaScript or TypeScript code you possibly can." |
| `strong` | element | *none* | text: "typescript-eslint enables ESLint to run on TypeScript code." |
| `div` | element | className="col col--offset-2 col--8" | <p> |
| `p` | element | *none* | text: "ESLint and TypeScript represent code differently internally.
            ESLint's default JavaScript parser cannot natively read in
            TypeScript-specific syntax and its rules don't natively have access
            to TypeScript's type information." |
| `div` | element | className="col col--offset-2 col--8" | text: "typescript-eslint:", <ul> |
| `ul` | element | *none* | <li>, <li>, <li> |
| `li` | element | *none* | text: "allows ESLint to parse TypeScript syntax" |
| `li` | element | *none* | text: "creates a set of tools for ESLint rules to be able to use
              TypeScript's type information" |
| `li` | element | *none* | text: "provides a large list of lint rules that are specific to
              TypeScript and/or use that type information" |
| `div` | element | className="col col--12 padding-vert--lg" | <div>, {description}, <div> |
| `div` | element | className="text--center" | <Heading> |
| `Heading` | component | as="h2", id={title.replaceAll(',', '').toLowerCase().replaceAll(/\s|_/g, '-')} | {title} |
| `div` | element | className={styles.buttons} | <Link> |
| `Link` | component | className={clsx('button button--primary', styles.buttonCentered)}, to={useBaseUrl('getting-started')} | text: "Get Started" |
| `Layout` | component | description={siteConfig.tagline} | <main> |
| `main` | element | *none* | <div>, {features.map((props, idx) => (
          <section
            className={clsx(
              styles.features,
              idx % 2 === 1 ? styles.lightBackground : '',
            )}
            key={idx}
          >
            <div className="container">
              <div className="row">
                <Feature {...props} />
              </div>
            </div>
          </section>
        ))}, <section> |
| `div` | element | className={clsx('hero hero--dark', styles.hero)} | <div> |
| `div` | element | className="container" | <img>, <h1>, <p>, <div> |
| `img` | element | alt="Hero Logo", className={styles.hero__logo}, src="/img/logo.svg" | *none* |
| `h1` | element | className="hero__title" | {siteConfig.title} |
| `p` | element | className="hero__subtitle" | {siteConfig.tagline} |
| `div` | element | className={styles.buttons} | <Link>, <Link> |
| `Link` | component | className="button button--primary", to={useBaseUrl('getting-started')} | text: "Get Started" |
| `Link` | component | className="button button--secondary button--outline", to={useBaseUrl('play/')} | text: "Playground" |
| `section` | element | className={clsx(
              styles.features,
              idx % 2 === 1 ? styles.lightBackground : '',
            )}, key={idx} | <div> |
| `div` | element | className="container" | <div> |
| `div` | element | className="row" | <Feature> |
| `Feature` | component | *none* | *none* |
| `section` | element | className={styles.sponsors} | <div> |
| `div` | element | className="container text--center padding-vert--lg" | <Heading>, <FinancialContributors> |
| `Heading` | component | as="h2", id="financial-contributors" | text: "Financial Contributors" |
| `FinancialContributors` | component | *none* | *none* |


---

## Functions

### `Feature({ description, title }: FeatureItem): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Feature({ description, title }: FeatureItem): React.JSX.Element {
  return (
    <div className="col col--12 padding-vert--lg">
      <div className="text--center">
        <Heading
          as="h2"
          id={title.replaceAll(',', '').toLowerCase().replaceAll(/\s|_/g, '-')}
        >
          {title}
        </Heading>
      </div>
      {description}
      <div className={styles.buttons}>
        <Link
          className={clsx('button button--primary', styles.buttonCentered)}
          to={useBaseUrl('getting-started')}
        >
          Get Started
        </Link>
      </div>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{ description, title }: FeatureItem`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `title.replaceAll(',', '').toLowerCase().replaceAll`
  - `clsx (from clsx)`
  - `useBaseUrl (from @docusaurus/useBaseUrl)`
### `Home(): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Home(): React.JSX.Element {
  const { siteConfig } = useDocusaurusContext();
  return (
    <Layout description={siteConfig.tagline}>
      <main>
        <div className={clsx('hero hero--dark', styles.hero)}>
          <div className="container">
            <img
              alt="Hero Logo"
              className={styles.hero__logo}
              src="/img/logo.svg"
            />
            <h1 className="hero__title">{siteConfig.title}</h1>
            <p className="hero__subtitle">{siteConfig.tagline}</p>
            <div className={styles.buttons}>
              <Link
                className="button button--primary"
                to={useBaseUrl('getting-started')}
              >
                Get Started
              </Link>
              <Link
                className="button button--secondary button--outline"
                to={useBaseUrl('play/')}
              >
                Playground
              </Link>
            </div>
          </div>
        </div>

        {features.map((props, idx) => (
          <section
            className={clsx(
              styles.features,
              idx % 2 === 1 ? styles.lightBackground : '',
            )}
            key={idx}
          >
            <div className="container">
              <div className="row">
                <Feature {...props} />
              </div>
            </div>
          </section>
        ))}
        <section className={styles.sponsors}>
          <div className="container text--center padding-vert--lg">
            <Heading as="h2" id="financial-contributors">
              Financial Contributors
            </Heading>
            <FinancialContributors />
          </div>
        </section>
      </main>
    </Layout>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useDocusaurusContext (from @docusaurus/useDocusaurusContext)`
  - `clsx (from clsx)`
  - `useBaseUrl (from @docusaurus/useBaseUrl)`
  - `features.map`

---

## Interfaces

### `FeatureItem`

<details><summary>Interface Code</summary>

```ts
interface FeatureItem {
  description: React.JSX.Element;
  imageUrl?: string;
  title: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `description` | `React.JSX.Element` | ✗ |  |
| `imageUrl` | `string` | ✓ |  |
| `title` | `string` | ✗ |  |


---