[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/website/src/components/editor/types.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `UpdateModel` | `../linter/types` |
| `ConfigModel` | `../types` |
| `ErrorGroup` | `../types` |
| `SelectedRange` | `../types` |
| `TabType` | `../types` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `CommonEditorProps`

<details><summary>Interface Code</summary>

```ts
export interface CommonEditorProps extends ConfigModel {
  readonly activeTab: TabType;
  readonly onASTChange: (value: UpdateModel | undefined) => void;
  readonly onChange: (cfg: Partial<ConfigModel>) => void;
  readonly onMarkersChange: (value: ErrorGroup[]) => void;
  readonly onSelect: (position?: number) => void;
  readonly selectedRange?: SelectedRange;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `activeTab` | `TabType` | ✗ |  |
| `onASTChange` | `(value: UpdateModel | undefined) => void` | ✗ |  |
| `onChange` | `(cfg: Partial<ConfigModel>) => void` | ✗ |  |
| `onMarkersChange` | `(value: ErrorGroup[]) => void` | ✗ |  |
| `onSelect` | `(position?: number) => void` | ✗ |  |
| `selectedRange` | `SelectedRange` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---