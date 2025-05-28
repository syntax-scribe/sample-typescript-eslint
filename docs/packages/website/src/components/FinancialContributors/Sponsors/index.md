[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 5 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Interfaces](#interfaces)

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

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={clsx(styles.tierArea, className)} | <h3>, <ul> |
| `h3` | element | *none* | {title} |
| `ul` | element | className={clsx(styles.sponsorsTier, styles[`tier-${tier}`])} | {sponsors.map(sponsor => (
          <li key={sponsor.id}>
            <Sponsor includeName={includeName} sponsor={sponsor} />
          </li>
        ))} |
| `li` | element | key={sponsor.id} | <Sponsor> |
| `Sponsor` | component | includeName={includeName}, sponsor={sponsor} | *none* |


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