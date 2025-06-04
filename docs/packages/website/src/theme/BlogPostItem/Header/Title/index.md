[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 2 |
| 💠 JSX Elements | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/theme/BlogPostItem/Header/Title/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Props` | `@theme/BlogPostItem/Header/Title` |
| `Link` | `@docusaurus/Link` |
| `useBlogPost` | `@docusaurus/plugin-content-blog/client` |
| `clsx` | `clsx` |
| `React` | `react` |
| `Markdown` | `react-markdown` |
| `styles` | `./styles.module.css` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `TitleHeading` | `"h1" | "h2"` | const | `isBlogPostPage ? 'h1' : 'h2'` | ✗ |
| `title` | `any` | const | `<Markdown>{titleRaw}</Markdown>` | ✗ |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Markdown` | component | *none* | {titleRaw} |
| `TitleHeading` | component | className={clsx(styles.title, className)} | {isBlogPostPage ? title : <Link to={permalink}>{title}</Link>} |
| `Link` | component | to={permalink} | {title} |


---

## Functions

### `BlogPostItemHeaderTitle({
  className,
}: Props): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function BlogPostItemHeaderTitle({
  className,
}: Props): React.JSX.Element {
  const { isBlogPostPage, metadata } = useBlogPost();
  const { permalink, title: titleRaw } = metadata;
  const TitleHeading = isBlogPostPage ? 'h1' : 'h2';
  const title = <Markdown>{titleRaw}</Markdown>;
  return (
    <TitleHeading className={clsx(styles.title, className)}>
      {isBlogPostPage ? title : <Link to={permalink}>{title}</Link>}
    </TitleHeading>
  );
}
```
</details>

- **Parameters**:
  - `{
  className,
}: Props`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `useBlogPost (from @docusaurus/plugin-content-blog/client)`
  - `clsx (from clsx)`

---