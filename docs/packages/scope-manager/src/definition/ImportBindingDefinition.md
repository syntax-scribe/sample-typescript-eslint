[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImportBindingDefinition.ts`

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