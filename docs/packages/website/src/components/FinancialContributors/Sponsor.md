[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Sponsor.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/FinancialContributors/Sponsor.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `React` | `react` |
| `SponsorData` | `./types` |
| `styles` | `./styles.module.css` |


---

## Functions

### `Sponsor({
  includeName,
  sponsor,
}: SponsorProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function Sponsor({
  includeName,
  sponsor,
}: SponsorProps): React.JSX.Element {
  let children = <img alt={`${sponsor.name} logo`} src={sponsor.image} />;

  if (includeName) {
    children = (
      <>
        {children}
        {sponsor.name.split(' - ')[0]}
      </>
    );
  }

  return (
    <Link
      className={styles.sponsorLink}
      href={sponsor.website}
      title={sponsor.name}
      rel="noopener sponsored"
    >
      {children}
    </Link>
  );
}
```
</details>

- **Parameters**:
  - `{
  includeName,
  sponsor,
}: SponsorProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `sponsor.name.split`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `SponsorProps`

<details><summary>Interface Code</summary>

```ts
interface SponsorProps {
  includeName?: boolean;
  sponsor: SponsorData;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `includeName` | `boolean` | ✓ |  |
| `sponsor` | `SponsorData` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---