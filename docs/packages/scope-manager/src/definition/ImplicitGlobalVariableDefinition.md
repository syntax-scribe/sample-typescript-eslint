[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImplicitGlobalVariableDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/ImplicitGlobalVariableDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## Classes

### `ImplicitGlobalVariableDefinition`

<details><summary>Class Code</summary>

```ts
export class ImplicitGlobalVariableDefinition extends DefinitionBase<
  DefinitionType.ImplicitGlobalVariable,
  TSESTree.Node,
  null,
  TSESTree.BindingName
> {
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;

  constructor(
    name: TSESTree.BindingName,
    node: ImplicitGlobalVariableDefinition['node'],
  ) {
    super(DefinitionType.ImplicitGlobalVariable, name, node, null);
  }
}
```
</details>


---