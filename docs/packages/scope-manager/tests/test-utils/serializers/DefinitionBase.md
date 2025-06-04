[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `DefinitionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/serializers/DefinitionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `../../../src/definition/DefinitionBase` |
| `createSerializer` | `./baseSerializer` |


---

## Classes

### `DefinitionInstance`

<details><summary>Class Code</summary>

```ts
class DefinitionInstance extends DefinitionBase<
  /* eslint-disable @typescript-eslint/no-explicit-any */
  any,
  any,
  any,
  /* eslint-enable @typescript-eslint/no-explicit-any */
  TSESTree.BindingName
> {
  isTypeDefinition = false;
  isVariableDefinition = false;
}
```
</details>


---