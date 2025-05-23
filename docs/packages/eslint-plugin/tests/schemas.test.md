[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `schemas.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/schemas.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `compile` | `@typescript-eslint/rule-schema-to-typescript-types` |
| `prettier` | `prettier` |
| `rules` | `../src/rules/index.js` |
| `areOptionsValid` | `./areOptionsValid.js` |


---

## Functions

### `getPrettierConfig(filepath: string): Promise<prettier.Options>`

<details><summary>Code</summary>

```ts
async (
  filepath: string,
): Promise<prettier.Options> => {
  const config = await prettier.resolveConfig(filepath, {
    config: PRETTIER_CONFIG_PATH,
  });
  if (config == null) {
    throw new Error('Unable to resolve prettier config');
  }
  return {
    ...config,
    filepath,
  };
}
```
</details>

- **Parameters**:
  - `filepath: string`
- **Return Type**: `Promise<prettier.Options>`
- **Calls**:
  - `prettier.resolveConfig`

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