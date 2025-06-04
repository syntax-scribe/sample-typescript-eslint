[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 6 |
| 💠 JSX Elements | 11 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/FinancialContributors/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `sponsors` | `@site/data/sponsors.json` |
| `clsx` | `clsx` |
| `React` | `react` |
| `Sponsors` | `./Sponsors` |
| `styles` | `./styles.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Fragment` | fragment | *none* | <p>, <div>, <div> |
| `p` | element | *none* | text: "The typescript-eslint project would not be possible without the generous
        support of our financial contributors." |
| `div` | element | className={styles.sponsorsContainer} | <Sponsors>, <Sponsors>, <Sponsors> |
| `Sponsors` | component | className={styles.tierSponsorArea}, includeName, sponsors={sponsors.slice(0, 6)}, tier="platinum-sponsor", title="Platinum Sponsors" | *none* |
| `Sponsors` | component | className={styles.tierSupporterArea}, sponsors={sponsors.slice(6, 16)}, tier="gold-supporter", title="Gold Supporters" | *none* |
| `Sponsors` | component | className={styles.tierOtherArea}, sponsors={sponsors.slice(16, 34)}, tier="silver-supporter", title="Silver Supporters" | *none* |
| `div` | element | className={styles.linksArea} | <Link>, <div> |
| `Link` | component | className={clsx('button button--primary', styles.become)}, target="_blank", to="https://opencollective.com/typescript-eslint/contribute" | text: "Become a financial sponsor" |
| `div` | element | className={styles.linksMore} | <Link>, <Link> |
| `Link` | component | className="button button--info button--outline", target="_blank", to="https://opencollective.com/typescript-eslint" | text: "See all financial sponsors" |
| `Link` | component | className="button button--info button--outline", target="_blank", title="Sponsorship docs", to="https://github.com/typescript-eslint/typescript-eslint/blob/main/.github/SPONSORSHIPS.md" | text: "Docs" |


---

## Functions

### `FinancialContributors(): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function FinancialContributors(): React.JSX.Element {
  return (
    <>
      <p>
        The typescript-eslint project would not be possible without the generous
        support of our financial contributors.
      </p>
      <div className={styles.sponsorsContainer}>
        <Sponsors
          className={styles.tierSponsorArea}
          includeName
          sponsors={sponsors.slice(0, 6)}
          tier="platinum-sponsor"
          title="Platinum Sponsors"
        />
        <Sponsors
          className={styles.tierSupporterArea}
          sponsors={sponsors.slice(6, 16)}
          tier="gold-supporter"
          title="Gold Supporters"
        />
        <Sponsors
          className={styles.tierOtherArea}
          sponsors={sponsors.slice(16, 34)}
          tier="silver-supporter"
          title="Silver Supporters"
        />
      </div>
      <div className={styles.linksArea}>
        <Link
          className={clsx('button button--primary', styles.become)}
          target="_blank"
          to="https://opencollective.com/typescript-eslint/contribute"
        >
          Become a financial sponsor
        </Link>
        <div className={styles.linksMore}>
          <Link
            className="button button--info button--outline"
            target="_blank"
            to="https://opencollective.com/typescript-eslint"
          >
            See all financial sponsors
          </Link>
          <Link
            className="button button--info button--outline"
            target="_blank"
            title="Sponsorship docs"
            to="https://github.com/typescript-eslint/typescript-eslint/blob/main/.github/SPONSORSHIPS.md"
          >
            Docs
          </Link>
        </div>
      </div>
    </>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `sponsors.slice`
  - `clsx (from clsx)`

---