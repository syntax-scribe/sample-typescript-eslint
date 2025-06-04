[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionNameDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 3 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/FunctionNameDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## Classes

### `FunctionNameDefinition`

<details><summary>Class Code</summary>

```ts
export class FunctionNameDefinition extends DefinitionBase<
  DefinitionType.FunctionName,
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | TSESTree.TSDeclareFunction
  | TSESTree.TSEmptyBodyFunctionExpression,
  null,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;

  constructor(name: TSESTree.Identifier, node: FunctionNameDefinition['node']) {
    super(DefinitionType.FunctionName, name, node, null);
  }
}
```
</details>


---