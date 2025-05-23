[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `WithScope.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 1
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/WithScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `ScopeManager` | `../ScopeManager` |
| `Scope` | `./Scope` |
| `assert` | `../assert` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Functions

### `WithScope.close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public override close(scopeManager: ScopeManager): Scope | null {
    if (this.shouldStaticallyClose()) {
      return super.close(scopeManager);
    }
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => this.delegateToUpperScope(ref));
    this.leftToResolve = null;
    return this.upper;
  }
```
</details>

- **Parameters**:
  - `scopeManager: ScopeManager`
- **Return Type**: `Scope | null`
- **Calls**:
  - `this.shouldStaticallyClose`
  - `super.close`
  - `assert (from ../assert)`
  - `this.leftToResolve.forEach`
  - `this.delegateToUpperScope`

---

## Classes

### `WithScope`

<details><summary>Class Code</summary>

```ts
export class WithScope extends ScopeBase<
  ScopeType.with,
  TSESTree.WithStatement,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: WithScope['upper'],
    block: WithScope['block'],
  ) {
    super(scopeManager, ScopeType.with, upperScope, block, false);
  }

  public override close(scopeManager: ScopeManager): Scope | null {
    if (this.shouldStaticallyClose()) {
      return super.close(scopeManager);
    }
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => this.delegateToUpperScope(ref));
    this.leftToResolve = null;
    return this.upper;
  }
}
```
</details>

#### Methods

##### `close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public override close(scopeManager: ScopeManager): Scope | null {
    if (this.shouldStaticallyClose()) {
      return super.close(scopeManager);
    }
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => this.delegateToUpperScope(ref));
    this.leftToResolve = null;
    return this.upper;
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