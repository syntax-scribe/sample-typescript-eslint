[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prism-include-languages.js`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/theme/prism-include-languages.js`**

## 📦 Imports

| Name | Source |
|------|--------|
| `siteConfig` | `@generated/docusaurus.config` |


---

## Functions

### `prismIncludeLanguages(PrismObject: any): void`

<details><summary>Code</summary>

```ts
export default function prismIncludeLanguages(PrismObject) {
  const {
    themeConfig: { prism },
  } = siteConfig;
  const { additionalLanguages } = prism;
  globalThis.Prism = PrismObject;

  additionalLanguages.forEach(lang => {
    // eslint-disable-next-line @typescript-eslint/no-require-imports
    require(`prismjs/components/prism-${lang}`);
  });
  // eslint-disable-next-line @typescript-eslint/no-require-imports
  require(`../prism/language/jsonc`);
  delete globalThis.Prism;
}
```
</details>

- **Parameters**:
  - `PrismObject: any`
- **Return Type**: `void`
- **Calls**:
  - `additionalLanguages.forEach`
  - `require`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-require-imports (x6)
```


---