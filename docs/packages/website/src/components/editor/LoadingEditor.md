[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `LoadingEditor.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 5 |
| 💠 JSX Elements | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [JSX Elements](#jsx-elements)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/LoadingEditor.tsx`**

## 📦 Imports

| Name | Source |
|------|--------|
| `React` | `react` |
| `CommonEditorProps` | `./types` |
| `SandboxServicesProps` | `./useSandboxServices` |
| `LoadedEditor` | `./LoadedEditor` |
| `useSandboxServices` | `./useSandboxServices` |


---

## JSX Elements

| Component | Type | Props | Children |
|-----------|------|-------|----------|
| `Fragment` | fragment | *none* | *none* |
| `LoadedEditor` | component | *none* | *none* |


---

## Functions

### `LoadingEditor(props: any): any`

<details><summary>Code</summary>

```ts
props => {
  const services = useSandboxServices(props);

  if (!services) {
    return null;
  }

  if (services instanceof Error) {
    return <>{services.stack}</>;
  }

  return <LoadedEditor {...props} {...services} />;
}
```
</details>

- **Parameters**:
  - `props: any`
- **Return Type**: `any`
- **Calls**:
  - `useSandboxServices (from ./useSandboxServices)`

---

## Type Aliases

### `LoadingEditorProps`

```ts
type LoadingEditorProps = CommonEditorProps & SandboxServicesProps;
```


---