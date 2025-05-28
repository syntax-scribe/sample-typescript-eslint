[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TeamBio.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 8 |
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
📂 **`packages/website/src/components/team/TeamBio.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./TeamBio.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `li` | element | className={styles.teamBio} | <img>, <div>, <ol> |
| `img` | element | alt="", className={styles.profilePhoto}, src={`/img/team/${username}.jpg`} | *none* |
| `div` | element | className={styles.texts} | <strong>, <p> |
| `strong` | element | className={styles.name} | {name} |
| `p` | element | className={styles.description} | {description} |
| `ol` | element | className={styles.services} | {[['github', `https://github.com/${username}`] as const, ...links]
          .sort(([a], [b]) => a.localeCompare(b))
          .map(([service, url]) => (
            <li key={service}>
              <a
                aria-label={`${service}-link`}
                className={`image-link ${service}-link social-link-icon ${styles.serviceIconLink}`}
                href={url}
                target="_blank"
              />
            </li>
          ))} |
| `li` | element | key={service} | <a> |
| `a` | element | aria-label={`${service}-link`}, className={`image-link ${service}-link social-link-icon ${styles.serviceIconLink}`}, href={url}, target="_blank" | *none* |


---

## Functions

### `TeamBio({
  description,
  links = [],
  name,
  username,
}: BioEntry): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function TeamBio({
  description,
  links = [],
  name,
  username,
}: BioEntry): React.JSX.Element {
  return (
    <li className={styles.teamBio}>
      <img
        alt=""
        className={styles.profilePhoto}
        src={`/img/team/${username}.jpg`}
      />
      <div className={styles.texts}>
        <strong className={styles.name}>{name}</strong>
        <p className={styles.description}> {description}</p>
      </div>
      <ol className={styles.services}>
        {[['github', `https://github.com/${username}`] as const, ...links]
          .sort(([a], [b]) => a.localeCompare(b))
          .map(([service, url]) => (
            <li key={service}>
              <a
                aria-label={`${service}-link`}
                className={`image-link ${service}-link social-link-icon ${styles.serviceIconLink}`}
                href={url}
                target="_blank"
              />
            </li>
          ))}
      </ol>
    </li>
  );
}
```
</details>

- **Parameters**:
  - `{
  description,
  links = [],
  name,
  username,
}: BioEntry`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `[['github', `https://github.com/${username}`] as const, ...links]
          .sort(([a], [b]) => a.localeCompare(b))
          .map`

---

## Interfaces

### `BioEntry`

<details><summary>Interface Code</summary>

```ts
export interface BioEntry {
  description: string;
  links?: [string, string][];
  name: string;
  username: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `description` | `string` | ✗ |  |
| `links` | `[string, string][]` | ✓ |  |
| `name` | `string` | ✗ |  |
| `username` | `string` | ✗ |  |


---