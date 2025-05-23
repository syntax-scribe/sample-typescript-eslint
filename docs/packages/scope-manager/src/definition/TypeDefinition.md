[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TypeDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/TypeDefinition.ts`**

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

### `TypeDefinition`

<details><summary>Class Code</summary>

```ts
export class TypeDefinition extends DefinitionBase<
  DefinitionType.Type,
  | TSESTree.TSInterfaceDeclaration
  | TSESTree.TSMappedType
  | TSESTree.TSTypeAliasDeclaration
  | TSESTree.TSTypeParameter,
  null,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = false;

  constructor(name: TSESTree.Identifier, node: TypeDefinition['node']) {
    super(DefinitionType.Type, name, node, null);
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