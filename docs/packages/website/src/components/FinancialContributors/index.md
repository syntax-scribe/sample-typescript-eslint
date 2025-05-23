[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---