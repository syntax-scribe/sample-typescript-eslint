[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSEnumMemberDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/TSEnumMemberDefinition.ts`**

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

### `TSEnumMemberDefinition`

<details><summary>Class Code</summary>

```ts
export class TSEnumMemberDefinition extends DefinitionBase<
  DefinitionType.TSEnumMember,
  TSESTree.TSEnumMember,
  null,
  TSESTree.Identifier | TSESTree.StringLiteral
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = true;

  constructor(
    name: TSESTree.Identifier | TSESTree.StringLiteral,
    node: TSEnumMemberDefinition['node'],
  ) {
    super(DefinitionType.TSEnumMember, name, node, null);
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