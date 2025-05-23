[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TeamBio.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/team/TeamBio.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `styles` | `./TeamBio.module.css` |


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

## Classes

> No classes found in this file.


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

## Type Aliases

> No type aliases found in this file.


---