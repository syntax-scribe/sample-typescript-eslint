[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `GlobalScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 1 |
| 📦 Imports | 12 |
| 📊 Variables & Constants | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/GlobalScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Reference` | `../referencer/Reference` |
| `ScopeManager` | `../ScopeManager` |
| `ImplicitLibVariableOptions` | `../variable` |
| `Variable` | `../variable` |
| `Scope` | `./Scope` |
| `assert` | `../assert` |
| `ImplicitGlobalVariableDefinition` | `../definition/ImplicitGlobalVariableDefinition` |
| `ImplicitLibVariable` | `../variable` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `info` | `ReferenceImplicitGlobal` | const | `ref.maybeImplicitGlobal` | ✗ |
| `node` | `TSESTree.BindingName` | const | `info.pattern` | ✗ |


---

## Functions

### `GlobalScope.close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public override close(scopeManager: ScopeManager): Scope | null {
    assert(this.leftToResolve);

    for (const ref of this.leftToResolve) {
      if (ref.maybeImplicitGlobal && !this.set.has(ref.identifier.name)) {
        // create an implicit global variable from assignment expression
        const info = ref.maybeImplicitGlobal;
        const node = info.pattern;
        if (node.type === AST_NODE_TYPES.Identifier) {
          this.defineVariable(
            node.name,
            this.implicit.set,
            this.implicit.variables,
            node,
            new ImplicitGlobalVariableDefinition(info.pattern, info.node),
          );
        }
      }
    }

    this.implicit.leftToBeResolved = this.leftToResolve;
    return super.close(scopeManager);
  }
```
</details>

- **Parameters**:
  - `scopeManager: ScopeManager`
- **Return Type**: `Scope | null`
- **Calls**:
  - `assert (from ../assert)`
  - `this.set.has`
  - `this.defineVariable`
  - `super.close`
- **Internal Comments**:
```
// create an implicit global variable from assignment expression (x2)
```

### `GlobalScope.defineImplicitVariable(name: string, options: ImplicitLibVariableOptions): void`

<details><summary>Code</summary>

```ts
public defineImplicitVariable(
    name: string,
    options: ImplicitLibVariableOptions,
  ): void {
    this.defineVariable(
      new ImplicitLibVariable(this, name, options),
      this.set,
      this.variables,
      null,
      null,
    );
  }
```
</details>

- **Parameters**:
  - `name: string`
  - `options: ImplicitLibVariableOptions`
- **Return Type**: `void`
- **Calls**:
  - `this.defineVariable`

---

## Classes

### `GlobalScope`

<details><summary>Class Code</summary>

```ts
export class GlobalScope extends ScopeBase<
  ScopeType.global,
  TSESTree.Program,
  /**
   * The global scope has no parent.
   */
  null
> {
  // note this is accessed in used in the legacy eslint-scope tests, so it can't be true private
  private readonly implicit: {
    readonly set: Map<string, Variable>;
    readonly variables: Variable[];
    /**
     * List of {@link Reference}s that are left to be resolved (i.e. which
     * need to be linked to the variable they refer to).
     */
    leftToBeResolved: Reference[];
  };

  constructor(scopeManager: ScopeManager, block: GlobalScope['block']) {
    super(scopeManager, ScopeType.global, null, block, false);
    this.implicit = {
      leftToBeResolved: [],
      set: new Map<string, Variable>(),
      variables: [],
    };
  }

  public override close(scopeManager: ScopeManager): Scope | null {
    assert(this.leftToResolve);

    for (const ref of this.leftToResolve) {
      if (ref.maybeImplicitGlobal && !this.set.has(ref.identifier.name)) {
        // create an implicit global variable from assignment expression
        const info = ref.maybeImplicitGlobal;
        const node = info.pattern;
        if (node.type === AST_NODE_TYPES.Identifier) {
          this.defineVariable(
            node.name,
            this.implicit.set,
            this.implicit.variables,
            node,
            new ImplicitGlobalVariableDefinition(info.pattern, info.node),
          );
        }
      }
    }

    this.implicit.leftToBeResolved = this.leftToResolve;
    return super.close(scopeManager);
  }

  public defineImplicitVariable(
    name: string,
    options: ImplicitLibVariableOptions,
  ): void {
    this.defineVariable(
      new ImplicitLibVariable(this, name, options),
      this.set,
      this.variables,
      null,
      null,
    );
  }
}
```
</details>

#### Methods

##### `close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public override close(scopeManager: ScopeManager): Scope | null {
    assert(this.leftToResolve);

    for (const ref of this.leftToResolve) {
      if (ref.maybeImplicitGlobal && !this.set.has(ref.identifier.name)) {
        // create an implicit global variable from assignment expression
        const info = ref.maybeImplicitGlobal;
        const node = info.pattern;
        if (node.type === AST_NODE_TYPES.Identifier) {
          this.defineVariable(
            node.name,
            this.implicit.set,
            this.implicit.variables,
            node,
            new ImplicitGlobalVariableDefinition(info.pattern, info.node),
          );
        }
      }
    }

    this.implicit.leftToBeResolved = this.leftToResolve;
    return super.close(scopeManager);
  }
```
</details>

##### `defineImplicitVariable(name: string, options: ImplicitLibVariableOptions): void`

<details><summary>Code</summary>

```ts
public defineImplicitVariable(
    name: string,
    options: ImplicitLibVariableOptions,
  ): void {
    this.defineVariable(
      new ImplicitLibVariable(this, name, options),
      this.set,
      this.variables,
      null,
      null,
    );
  }
```
</details>


---