[⬅️ Back to Table of Contents](../../../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---