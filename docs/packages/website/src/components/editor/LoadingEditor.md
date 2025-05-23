[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `LoadingEditor.tsx`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 1

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `LoadingEditorProps`

```ts
type LoadingEditorProps = CommonEditorProps & SandboxServicesProps;
```


---