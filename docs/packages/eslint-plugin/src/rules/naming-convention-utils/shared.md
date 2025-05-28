[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `shared.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention-utils/shared.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `IndividualAndMetaSelectorsString` | `./enums` |
| `MetaSelectorsString` | `./enums` |
| `Selectors` | `./enums` |
| `SelectorsString` | `./enums` |
| `MetaSelectors` | `./enums` |


---

## Functions

### `selectorTypeToMessageString(selectorType: SelectorsString): string`

<details><summary>Code</summary>

```ts
export function selectorTypeToMessageString(
  selectorType: SelectorsString,
): string {
  const notCamelCase = selectorType.replaceAll(/([A-Z])/g, ' $1');
  return notCamelCase.charAt(0).toUpperCase() + notCamelCase.slice(1);
}
```
</details>

- **Parameters**:
  - `selectorType: SelectorsString`
- **Return Type**: `string`
- **Calls**:
  - `selectorType.replaceAll`
  - `notCamelCase.charAt(0).toUpperCase`
  - `notCamelCase.slice`
### `isMetaSelector(selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors): selector is MetaSelectorsString`

<details><summary>Code</summary>

```ts
export function isMetaSelector(
  selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors,
): selector is MetaSelectorsString {
  return selector in MetaSelectors;
}
```
</details>

- **Parameters**:
  - `selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors`
- **Return Type**: `selector is MetaSelectorsString`
### `isMethodOrPropertySelector(selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors): boolean`

<details><summary>Code</summary>

```ts
export function isMethodOrPropertySelector(
  selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors,
): boolean {
  return (
    selector === MetaSelectors.method || selector === MetaSelectors.property
  );
}
```
</details>

- **Parameters**:
  - `selector: IndividualAndMetaSelectorsString | MetaSelectors | Selectors`
- **Return Type**: `boolean`

---