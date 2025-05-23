[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `play.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---