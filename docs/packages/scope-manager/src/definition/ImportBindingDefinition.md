[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImportBindingDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/ImportBindingDefinition.ts`**

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

### `ImportBindingDefinition`

<details><summary>Class Code</summary>

```ts
export class ImportBindingDefinition extends DefinitionBase<
  DefinitionType.ImportBinding,
  | TSESTree.ImportDefaultSpecifier
  | TSESTree.ImportNamespaceSpecifier
  | TSESTree.ImportSpecifier
  | TSESTree.TSImportEqualsDeclaration,
  TSESTree.ImportDeclaration | TSESTree.TSImportEqualsDeclaration,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = true;

  constructor(
    name: TSESTree.Identifier,
    node: TSESTree.TSImportEqualsDeclaration,
    decl: TSESTree.TSImportEqualsDeclaration,
  );
  constructor(
    name: TSESTree.Identifier,
    node: Exclude<
      ImportBindingDefinition['node'],
      TSESTree.TSImportEqualsDeclaration
    >,
    decl: TSESTree.ImportDeclaration,
  );
  constructor(
    name: TSESTree.Identifier,
    node: ImportBindingDefinition['node'],
    decl: TSESTree.ImportDeclaration | TSESTree.TSImportEqualsDeclaration,
  ) {
    super(DefinitionType.ImportBinding, name, node, decl);
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