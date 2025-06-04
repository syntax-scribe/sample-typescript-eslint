[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `BlockScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/BlockScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ScopeManager` | `../ScopeManager` |
| `Scope` | `./Scope` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Classes

### `BlockScope`

<details><summary>Class Code</summary>

```ts
export class BlockScope extends ScopeBase<
  ScopeType.block,
  TSESTree.BlockStatement,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: BlockScope['upper'],
    block: BlockScope['block'],
  ) {
    super(scopeManager, ScopeType.block, upperScope, block, false);
  }
}
```
</details>


---