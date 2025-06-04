[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 📦 Imports | 9 |
| 💠 JSX Elements | 8 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/theme/BlogSidebar/Content/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Props` | `@theme/BlogSidebar/Content` |
| `ReactNode` | `react` |
| `groupBlogSidebarItemsByYear` | `@docusaurus/plugin-content-blog/client` |
| `useThemeConfig` | `@docusaurus/theme-common` |
| `Heading` | `@theme/Heading` |
| `memo` | `react` |
| `React` | `react` |
| `Markdown` | `react-markdown` |
| `styles` | `./styles.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | className={styles.blogSidebarContent}, role="group" | <Heading>, {children} |
| `Heading` | component | as="h3", className={yearGroupHeadingClassName} | {year} |
| `Markdown` | component | *none* | {item.title} |
| `Fragment` | fragment | *none* | *none* |
| `BlogSidebarYearGroup` | component | key={year}, year={year}, yearGroupHeadingClassName={yearGroupHeadingClassName} | <ListComponent> |
| `ListComponent` | component | items={yearItems} | *none* |
| `div` | element | className={styles.blogSidebarContent} | <ListComponent> |
| `ListComponent` | component | items={items} | *none* |


---

## Functions

### `BlogSidebarYearGroup({
  children,
  year,
  yearGroupHeadingClassName,
}: {
  children: ReactNode;
  year: string;
  yearGroupHeadingClassName?: string;
}): React.JSX.Element`

<details><summary>Code</summary>

```ts
function BlogSidebarYearGroup({
  children,
  year,
  yearGroupHeadingClassName,
}: {
  children: ReactNode;
  year: string;
  yearGroupHeadingClassName?: string;
}): React.JSX.Element {
  return (
    <div className={styles.blogSidebarContent} role="group">
      <Heading as="h3" className={yearGroupHeadingClassName}>
        {year}
      </Heading>
      {children}
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  children,
  year,
  yearGroupHeadingClassName,
}: {
  children: ReactNode;
  year: string;
  yearGroupHeadingClassName?: string;
}`
- **Return Type**: `React.JSX.Element`
### `BlogSidebarContent({
  items: itemsRaw,
  ListComponent,
  yearGroupHeadingClassName,
}: Props): ReactNode`

<details><summary>Code</summary>

```ts
function BlogSidebarContent({
  items: itemsRaw,
  ListComponent,
  yearGroupHeadingClassName,
}: Props): ReactNode {
  const items = itemsRaw.map(item => ({
    ...item,
    title: (<Markdown>{item.title}</Markdown>) as unknown as string,
  }));

  const themeConfig = useThemeConfig();

  if (themeConfig.blog.sidebar.groupByYear) {
    const itemsByYear = groupBlogSidebarItemsByYear(items);
    return (
      <>
        {itemsByYear.map(([year, yearItems]) => (
          <BlogSidebarYearGroup
            key={year}
            year={year}
            yearGroupHeadingClassName={yearGroupHeadingClassName}
          >
            <ListComponent items={yearItems} />
          </BlogSidebarYearGroup>
        ))}
      </>
    );
  }

  return (
    <div className={styles.blogSidebarContent}>
      <ListComponent items={items} />
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  items: itemsRaw,
  ListComponent,
  yearGroupHeadingClassName,
}: Props`
- **Return Type**: `ReactNode`
- **Calls**:
  - `itemsRaw.map`
  - `useThemeConfig (from @docusaurus/theme-common)`
  - `groupBlogSidebarItemsByYear (from @docusaurus/plugin-content-blog/client)`
  - `itemsByYear.map`

---