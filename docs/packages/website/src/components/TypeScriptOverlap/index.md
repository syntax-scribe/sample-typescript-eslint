[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `index.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/TypeScriptOverlap/index.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Admonition` | `@theme/Admonition` |
| `React` | `react` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---