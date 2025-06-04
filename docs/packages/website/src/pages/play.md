[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `play.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 6 |
| 💠 JSX Elements | 6 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/pages/play.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `BrowserOnly` | `@docusaurus/BrowserOnly` |
| `Loader` | `@site/src/components/layout/Loader` |
| `Layout` | `@theme/Layout` |
| `lazy` | `react` |
| `Suspense` | `react` |
| `React` | `react` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Layout` | component | description="Playground", noFooter={true}, title="Playground" | <BrowserOnly> |
| `BrowserOnly` | component | fallback={<Loader />} | {(): React.JSX.Element => {
          return (
            <Suspense fallback={<Loader />}>
              <Playground />
            </Suspense>
          );
        }} |
| `Loader` | component | *none* | *none* |
| `Suspense` | component | fallback={<Loader />} | <Playground> |
| `Loader` | component | *none* | *none* |
| `Playground` | component | *none* | *none* |


---

## Functions

### `Play(): React.JSX.Element`

<details><summary>Code</summary>

```ts
function Play(): React.JSX.Element {
  return (
    <Layout description="Playground" noFooter={true} title="Playground">
      <BrowserOnly fallback={<Loader />}>
        {(): React.JSX.Element => {
          return (
            <Suspense fallback={<Loader />}>
              <Playground />
            </Suspense>
          );
        }}
      </BrowserOnly>
    </Layout>
  );
}
```
</details>

- **Return Type**: `React.JSX.Element`

---