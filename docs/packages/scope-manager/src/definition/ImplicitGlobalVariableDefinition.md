[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImplicitGlobalVariableDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/ImplicitGlobalVariableDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## 🔧 Functions

> No functions found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---