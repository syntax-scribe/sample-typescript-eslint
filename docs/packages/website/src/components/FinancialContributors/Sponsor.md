[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `Sponsor.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 3 |
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
📂 **`packages/website/src/components/FinancialContributors/Sponsor.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `React` | `react` |
| `SponsorData` | `./types` |
| `styles` | `./styles.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `children` | `any` | let/var | `<img alt={`${sponsor.name} logo`} src={sponsor.image} />` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `img` | element | alt={`${sponsor.name} logo`}, src={sponsor.image} | *none* |
| `Fragment` | fragment | *none* | *none* |
| `Link` | component | className={styles.sponsorLink}, href={sponsor.website}, title={sponsor.name}, rel="noopener sponsored" | {children} |


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