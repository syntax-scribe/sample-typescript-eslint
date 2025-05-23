[⬅️ Back to Table of Contents](../../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 9
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---