[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `DefinitionBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/serializers/DefinitionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `../../../src/definition/DefinitionBase` |
| `createSerializer` | `./baseSerializer` |


---

## 🔧 Functions

> No functions found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---