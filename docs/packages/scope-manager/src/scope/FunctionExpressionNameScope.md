[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionExpressionNameScope.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

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

## 🔧 Functions

> No functions found in this file.


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

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---