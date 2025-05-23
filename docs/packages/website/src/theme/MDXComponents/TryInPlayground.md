[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `TryInPlayground.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/theme/MDXComponents/TryInPlayground.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Link` | `@docusaurus/Link` |
| `clsx` | `clsx` |
| `React` | `react` |
| `fileTypes` | `../../components/options` |
| `styles` | `./TryInPlayground.module.css` |


---

## Functions

### `TryInPlayground({
  children,
  className,
  codeHash,
  eslintrcHash,
  language,
}: {
  children?: React.ReactNode;
  className?: string;
  codeHash?: string;
  eslintrcHash: string;
  language?: string;
}): React.ReactNode`

<details><summary>Code</summary>

```ts
export function TryInPlayground({
  children,
  className,
  codeHash,
  eslintrcHash,
  language,
}: {
  children?: React.ReactNode;
  className?: string;
  codeHash?: string;
  eslintrcHash: string;
  language?: string;
}): React.ReactNode {
  const params = new URLSearchParams({ eslintrc: eslintrcHash });
  if (codeHash) {
    params.set('code', codeHash);
  }
  if (language) {
    // iterating over sorted array, so the longer extensions will be matched first
    for (const [
      fileExtension,
      fileLanguageRegExp,
    ] of fileExtensionsSortedByLength) {
      if (fileLanguageRegExp.test(language)) {
        params.set('fileType', `.${fileExtension}`);
        break;
      }
    }
  }

  return (
    <Link
      className={clsx(styles.tryInPlaygroundLink, className)}
      target="_blank"
      to={`/play#${params.toString()}`}
    >
      {children}
    </Link>
  );
}
```
</details>

- **Parameters**:
  - `{
  children,
  className,
  codeHash,
  eslintrcHash,
  language,
}: {
  children?: React.ReactNode;
  className?: string;
  codeHash?: string;
  eslintrcHash: string;
  language?: string;
}`
- **Return Type**: `React.ReactNode`
- **Calls**:
  - `params.set`
  - `fileLanguageRegExp.test`
  - `clsx (from clsx)`
  - `params.toString`
- **Internal Comments**:
```
// iterating over sorted array, so the longer extensions will be matched first
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