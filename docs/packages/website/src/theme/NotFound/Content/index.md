[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 10 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/theme/NotFound/Content/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `useLocation` | `@docusaurus/router` |
| `React` | `react` |
| `styles` | `./styles.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `pathNameQuoted` | `string[]` | const | `[...`'${location.pathname}'`]` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `main` | element | className="container margin-vert--xl" | <div> |
| `div` | element | className="row" | <div> |
| `div` | element | className="col col--8 col--offset-2" | <h1>, <p>, <p> |
| `h1` | element | className={styles.title} | <div>, <strong>, {' '}, text: "is not defined." |
| `div` | element | className={styles.code} | text: "$ npx eslint ." |
| `strong` | element | *none* | {pathNameQuoted.map((letter, i) => (
                <span className={styles.word} key={i}>
                  {letter}
                </span>
              ))} |
| `span` | element | className={styles.word}, key={i} | {letter} |
| `p` | element | className="hero__subtitle" | text: "Looks like the page you're looking for doesn't exist. 😥" |
| `p` | element | *none* | text: "If you were linked here within typescript-eslint.io, there's
            probably a bug in the site. Please", {' '}, <a>, text: "." |
| `a` | element | href="https://github.com/typescript-eslint/typescript-eslint/issues/new/choose" | text: "file an issue on GitHub" |


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