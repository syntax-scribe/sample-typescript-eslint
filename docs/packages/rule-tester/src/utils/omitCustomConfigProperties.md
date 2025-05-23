[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `omitCustomConfigProperties.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 1
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/omitCustomConfigProperties.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTesterConfig` | `../types/RuleTesterConfig` |


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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---