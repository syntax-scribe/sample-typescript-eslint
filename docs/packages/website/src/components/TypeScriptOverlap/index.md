[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `index.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |
| 💠 JSX Elements | 7 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/website/src/components/TypeScriptOverlap/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Admonition` | `@theme/Admonition` |
| `React` | `react` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `div` | element | *none* | <Admonition> |
| `Admonition` | component | type="danger" | <p>, {strict == null ? (
          <></>
        ) : (
          <p>
            (Note that technically, TypeScript will only catch this if you have
            the <code>strict</code> or <code>noImplicitThis</code> flags
            enabled. These are enabled in most TypeScript projects, since they
            are considered to be best practice.)
          </p>
        )} |
| `p` | element | *none* | text: "The code problem checked by this ESLint rule is automatically checked
          by the TypeScript compiler. Thus, it is not recommended to turn on
          this rule in new TypeScript projects. You only need to enable this
          rule if you prefer the ESLint error messages over the TypeScript
          compiler error messages." |
| `Fragment` | fragment | *none* | *none* |
| `p` | element | *none* | text: "(Note that technically, TypeScript will only catch this if you have
            the", <code>, text: "or", <code>, text: "flags
            enabled. These are enabled in most TypeScript projects, since they
            are considered to be best practice.)" |
| `code` | element | *none* | text: "strict" |
| `code` | element | *none* | text: "noImplicitThis" |


---

## Functions

### `TypeScriptOverlap({
  strict,
}: {
  strict?: string;
}): React.JSX.Element`

<details><summary>Code</summary>

```ts
export default function TypeScriptOverlap({
  strict,
}: {
  strict?: string;
}): React.JSX.Element {
  return (
    <div>
      <Admonition type="danger">
        <p>
          The code problem checked by this ESLint rule is automatically checked
          by the TypeScript compiler. Thus, it is not recommended to turn on
          this rule in new TypeScript projects. You only need to enable this
          rule if you prefer the ESLint error messages over the TypeScript
          compiler error messages.
        </p>
        {strict == null ? (
          <></>
        ) : (
          <p>
            (Note that technically, TypeScript will only catch this if you have
            the <code>strict</code> or <code>noImplicitThis</code> flags
            enabled. These are enabled in most TypeScript projects, since they
            are considered to be best practice.)
          </p>
        )}
      </Admonition>
    </div>
  );
}
```
</details>

- **Parameters**:
  - `{
  strict,
}: {
  strict?: string;
}`
- **Return Type**: `React.JSX.Element`

---