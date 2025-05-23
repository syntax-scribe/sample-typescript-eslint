[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/FinancialContributors/Sponsors/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `clsx` | `clsx` |
| `React` | `react` |
| `SponsorData` | `../types` |
| `Sponsor` | `../Sponsor` |
| `styles` | `./styles.module.css` |


---

## Functions

### `Sponsors({
  className,
  includeName,
  sponsors,
  tier,
  title,
}: SponsorsProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function Sponsors({
  className,
  includeName,
  sponsors,
  tier,
  title,
}: SponsorsProps): React.JSX.Element {
  return (
    <div className={clsx(styles.tierArea, className)}>
      <h3>{title}</h3>
      <ul className={clsx(styles.sponsorsTier, styles[`tier-${tier}`])}>
        {sponsors.map(sponsor => (
          <li key={sponsor.id}>
            <Sponsor includeName={includeName} sponsor={sponsor} />
          </li>
        ))}
      </ul>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  className,
  includeName,
  sponsors,
  tier,
  title,
}: SponsorsProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `clsx (from clsx)`
  - `sponsors.map`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `SponsorsProps`

<details><summary>Interface Code</summary>

```ts
interface SponsorsProps {
  className: string;
  expanded?: boolean;
  includeName?: boolean;
  sponsors: SponsorData[];
  tier: string;
  title: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `className` | `string` | ✗ |  |
| `expanded` | `boolean` | ✓ |  |
| `includeName` | `boolean` | ✓ |  |
| `sponsors` | `SponsorData[]` | ✗ |  |
| `tier` | `string` | ✗ |  |
| `title` | `string` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---