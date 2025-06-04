[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassStaticBlockScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🧱 Classes | 1 |
| 📦 Imports | 5 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/ClassStaticBlockScope.ts`**

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

### `ClassStaticBlockScope`

<details><summary>Class Code</summary>

```ts
export class ClassStaticBlockScope extends ScopeBase<
  ScopeType.classStaticBlock,
  TSESTree.StaticBlock,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: ClassStaticBlockScope['upper'],
    block: ClassStaticBlockScope['block'],
  ) {
    super(scopeManager, ScopeType.classStaticBlock, upperScope, block, false);
  }
}
```
</details>


---