[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `DefinitionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 3 |
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