[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

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