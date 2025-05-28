[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `PackageLink.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 1 |
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
📂 **`packages/website/src/theme/MDXComponents/PackageLink.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `packageData` | `@typescript-eslint/parser/package.json` |
| `Npm` | `@uiw/react-shields/npm` |
| `React` | `react` |
| `styles` | `./PackageLink.module.css` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Npm.Version` | component | alt={`npm: ${fullPackageName} v${version}`}, anchor={{ target: '_blank' }}, className={styles.packageLink}, href={`https://npmjs.com/${fullPackageName}`}, packageName={packageName}, scope={scope} | *none* |


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