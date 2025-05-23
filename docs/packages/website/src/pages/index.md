[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 9
- **Interfaces**: 1
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---