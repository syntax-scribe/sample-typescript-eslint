[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSEnumNameDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/TSEnumNameDefinition.ts`**

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

### `TSEnumNameDefinition`

<details><summary>Class Code</summary>

```ts
export class TSEnumNameDefinition extends DefinitionBase<
  DefinitionType.TSEnumName,
  TSESTree.TSEnumDeclaration,
  null,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = true;

  constructor(name: TSESTree.Identifier, node: TSEnumNameDefinition['node']) {
    super(DefinitionType.TSEnumName, name, node, null);
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