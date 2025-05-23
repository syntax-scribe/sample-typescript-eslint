[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PackageLink.tsx`

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
📂 **`packages/website/src/theme/MDXComponents/PackageLink.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `packageData` | `@typescript-eslint/parser/package.json` |
| `Npm` | `@uiw/react-shields/npm` |
| `React` | `react` |
| `styles` | `./PackageLink.module.css` |


---

## Functions

### `PackageLink({
  packageName,
  scope,
}: PackageLinkProps): React.JSX.Element`

<details><summary>Code</summary>

```ts
export function PackageLink({
  packageName,
  scope,
}: PackageLinkProps): React.JSX.Element {
  const fullPackageName = [scope, packageName].filter(Boolean).join('/');
  const { version } = packageData;

  return (
    <Npm.Version
      alt={`npm: ${fullPackageName} v${version}`}
      anchor={{ target: '_blank' }}
      className={styles.packageLink}
      href={`https://npmjs.com/${fullPackageName}`}
      packageName={packageName}
      scope={scope}
    />
  );
}
```
</details>

- **Parameters**:
  - `{
  packageName,
  scope,
}: PackageLinkProps`
- **Return Type**: `React.JSX.Element`
- **Calls**:
  - `[scope, packageName].filter(Boolean).join`

---

## Classes

> No classes found in this file.


---

## Interfaces

### `PackageLinkProps`

<details><summary>Interface Code</summary>

```ts
export interface PackageLinkProps {
  packageName: string;
  scope?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `packageName` | `string` | ✗ |  |
| `scope` | `string` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---