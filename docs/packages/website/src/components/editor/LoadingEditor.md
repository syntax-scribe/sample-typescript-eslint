[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `LoadingEditor.tsx`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 2 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

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