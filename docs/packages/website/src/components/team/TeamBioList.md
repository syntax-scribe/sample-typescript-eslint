[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TeamBioList.tsx`

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
📂 **`packages/website/src/components/team/TeamBioList.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `BioEntry` | `./TeamBio` |
| `TeamBio` | `./TeamBio` |
| `styles` | `./TeamBioList.module.css` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---