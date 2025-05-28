[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TeamBioList.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 6 |
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
📂 **`packages/website/src/components/team/TeamBioList.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `BioEntry` | `./TeamBio` |
| `TeamBio` | `./TeamBio` |
| `styles` | `./TeamBioList.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.teamBioList} | <div>, <ul> |
| `div` | element | className={styles.texts} | <p>, <p> |
| `p` | element | className={styles.description} | {description} |
| `p` | element | className={styles.explanation} | {explanation} |
| `ul` | element | className={styles.bios} | {bios.map(bio => (
          <TeamBio {...bio} key={bio.name} />
        ))} |
| `TeamBio` | component | key={bio.name} | *none* |


---

## Functions

### `TeamBioList({
  bios,
  description,
  explanation,
}: TeamBioListProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function TeamBioList({
  bios,
  description,
  explanation,
}: TeamBioListProps): React.JSX.Element {
  return (
    <div className={styles.teamBioList}>
      <div className={styles.texts}>
        <p className={styles.description}>{description}</p>
        <p className={styles.explanation}>{explanation}</p>
      </div>
      <ul className={styles.bios}>
        {bios.map(bio => (
          <TeamBio {...bio} key={bio.name} />
        ))}
      </ul>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  bios,
  description,
  explanation,
}: TeamBioListProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `bios.map`

---

## Interfaces

### `TeamBioListProps`

<details><summary>Interface Code</summary>

```ts
export interface TeamBioListProps {
  bios: BioEntry[];
  description: string;
  explanation: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `bios` | `BioEntry[]` | ✗ |  |
| `description` | `string` | ✗ |  |
| `explanation` | `string` | ✗ |  |


---