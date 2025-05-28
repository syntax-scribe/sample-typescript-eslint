[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `omitCustomConfigProperties.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 1 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/omitCustomConfigProperties.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTesterConfig` | `../types/RuleTesterConfig` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `copy` | `{ defaultFilenames?: Readonly<{ ts: string; tsx: string; }>; dependencyConstraints?: Readonly<Record<string, VersionConstraint>>; }` | const | `{ ...config }` | ✗ |


---

## Functions

### `omitCustomConfigProperties(config: Partial<RuleTesterConfig>): Omit<typeof config, 'defaultFilenames'>`

<details><summary>Code</summary>

```ts
export function omitCustomConfigProperties(
  config: Partial<RuleTesterConfig>,
): Omit<typeof config, 'defaultFilenames'> {
  const copy = { ...config };

  delete copy.defaultFilenames;
  delete copy.dependencyConstraints;

  return copy;
}
```
</details>

- **Parameters**:
  - `config: Partial<RuleTesterConfig>`
- **Return Type**: `Omit<typeof config, 'defaultFilenames'>`

---