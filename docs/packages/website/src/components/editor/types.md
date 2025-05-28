[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `types.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

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

## 🔧 Functions

> No functions found in this file.


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