[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionExpressionNameScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 6 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/FunctionExpressionNameScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ScopeManager` | `../ScopeManager` |
| `Scope` | `./Scope` |
| `FunctionNameDefinition` | `../definition` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Classes

### `FunctionExpressionNameScope`

<details><summary>Class Code</summary>

```ts
export class FunctionExpressionNameScope extends ScopeBase<
  ScopeType.functionExpressionName,
  TSESTree.FunctionExpression,
  Scope
> {
  public override readonly functionExpressionScope: true;

  constructor(
    scopeManager: ScopeManager,
    upperScope: FunctionExpressionNameScope['upper'],
    block: FunctionExpressionNameScope['block'],
  ) {
    super(
      scopeManager,
      ScopeType.functionExpressionName,
      upperScope,
      block,
      false,
    );
    if (block.id) {
      this.defineIdentifier(
        block.id,
        new FunctionNameDefinition(block.id, block),
      );
    }
    this.functionExpressionScope = true;
  }
}
```
</details>


---