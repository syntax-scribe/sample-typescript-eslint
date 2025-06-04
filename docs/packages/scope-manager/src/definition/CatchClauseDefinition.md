[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `CatchClauseDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/CatchClauseDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## Classes

### `CatchClauseDefinition`

<details><summary>Class Code</summary>

```ts
export class CatchClauseDefinition extends DefinitionBase<
  DefinitionType.CatchClause,
  TSESTree.CatchClause,
  null,
  TSESTree.BindingName
> {
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;

  constructor(name: TSESTree.BindingName, node: CatchClauseDefinition['node']) {
    super(DefinitionType.CatchClause, name, node, null);
  }
}
```
</details>


---