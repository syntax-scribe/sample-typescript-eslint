[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSModuleNameDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/TSModuleNameDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## Classes

### `TSModuleNameDefinition`

<details><summary>Class Code</summary>

```ts
export class TSModuleNameDefinition extends DefinitionBase<
  DefinitionType.TSModuleName,
  TSESTree.TSModuleDeclaration,
  null,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = true;

  constructor(name: TSESTree.Identifier, node: TSModuleNameDefinition['node']) {
    super(DefinitionType.TSModuleName, name, node, null);
  }
}
```
</details>


---