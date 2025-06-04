[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `VariableDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/VariableDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


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