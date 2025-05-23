[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/theme/NotFound/Content/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useLocation` | `@docusaurus/router` |
| `React` | `react` |
| `styles` | `./styles.module.css` |


---

## Functions

### `NotFound(): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function NotFound(): React.JSX.Element {
  const location = useLocation();

  // https://github.com/sindresorhus/eslint-plugin-unicorn/issues/2521
  // eslint-disable-next-line @typescript-eslint/no-misused-spread
  const pathNameQuoted = [...`'${location.pathname}'`];

  return (
    <main className="container margin-vert--xl">
      <div className="row">
        <div className="col col--8 col--offset-2">
          <h1 className={styles.title}>
            <div className={styles.code}>$ npx eslint .</div>
            <strong>
              {pathNameQuoted.map((letter, i) => (
                <span className={styles.word} key={i}>
                  {letter}
                </span>
              ))}
            </strong>{' '}
            is not defined.
          </h1>
          <p className="hero__subtitle">
            Looks like the page you're looking for doesn't exist. 😥
          </p>
          <p>
            If you were linked here within typescript-eslint.io, there's
            probably a bug in the site. Please{' '}
            <a href="https://github.com/typescript-eslint/typescript-eslint/issues/new/choose">
              file an issue on GitHub
            </a>
            .
          </p>
        </div>
      </div>
    </main>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useLocation (from @docusaurus/router)`
  - `pathNameQuoted.map`
- **Internal Comments**:
```
// https://github.com/sindresorhus/eslint-plugin-unicorn/issues/2521 (x2)
// eslint-disable-next-line @typescript-eslint/no-misused-spread (x2)
```


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