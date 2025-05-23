[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `VariableDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/VariableDefinition.ts`**

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

### `VariableDefinition`

<details><summary>Class Code</summary>

```ts
export class VariableDefinition extends DefinitionBase<
  DefinitionType.Variable,
  TSESTree.VariableDeclarator,
  TSESTree.VariableDeclaration,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;

  constructor(
    name: TSESTree.Identifier,
    node: VariableDefinition['node'],
    decl: TSESTree.VariableDeclaration,
  ) {
    super(DefinitionType.Variable, name, node, decl);
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