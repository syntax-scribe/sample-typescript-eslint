[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionScope.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 1 |
| 📦 Imports | 8 |
| 📊 Variables & Constants | 1 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/FunctionScope.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Reference` | `../referencer/Reference` |
| `ScopeManager` | `../ScopeManager` |
| `Variable` | `../variable` |
| `Scope` | `./Scope` |
| `ScopeBase` | `./ScopeBase` |
| `ScopeType` | `./ScopeType` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `bodyStart` | `any` | const | `this.block.body?.range[0] ?? -1` | ✗ |


---

## Functions

### `FunctionScope.isValidResolution(ref: Reference, variable: Variable): boolean`

<details><summary>Code</summary>

```ts
protected override isValidResolution(
    ref: Reference,
    variable: Variable,
  ): boolean {
    // If `options.globalReturn` is true, `this.block` becomes a Program node.
    if (this.block.type === AST_NODE_TYPES.Program) {
      return true;
    }

    const bodyStart = this.block.body?.range[0] ?? -1;

    // It's invalid resolution in the following case:
    return !(
      (
        variable.scope === this &&
        ref.identifier.range[0] < bodyStart && // the reference is in the parameter part.
        variable.defs.every(d => d.name.range[0] >= bodyStart)
      ) // the variable is in the body.
    );
  }
```
</details>

- **Parameters**:
  - `ref: Reference`
  - `variable: Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `variable.defs.every`
- **Internal Comments**:
```
// If `options.globalReturn` is true, `this.block` becomes a Program node.
// It's invalid resolution in the following case:
```


---

## Classes

### `FunctionScope`

<details><summary>Class Code</summary>

```ts
export class FunctionScope extends ScopeBase<
  ScopeType.function,
  | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | TSESTree.Program
  | TSESTree.TSDeclareFunction
  | TSESTree.TSEmptyBodyFunctionExpression,
  Scope
> {
  constructor(
    scopeManager: ScopeManager,
    upperScope: FunctionScope['upper'],
    block: FunctionScope['block'],
    isMethodDefinition: boolean,
  ) {
    super(
      scopeManager,
      ScopeType.function,
      upperScope,
      block,
      isMethodDefinition,
    );

    // section 9.2.13, FunctionDeclarationInstantiation.
    // NOTE Arrow functions never have an arguments objects.
    if (this.block.type !== AST_NODE_TYPES.ArrowFunctionExpression) {
      this.defineVariable('arguments', this.set, this.variables, null, null);
    }
  }

  // References in default parameters isn't resolved to variables which are in their function body.
  //     const x = 1
  //     function f(a = x) { // This `x` is resolved to the `x` in the outer scope.
  //         const x = 2
  //         console.log(a)
  //     }
  protected override isValidResolution(
    ref: Reference,
    variable: Variable,
  ): boolean {
    // If `options.globalReturn` is true, `this.block` becomes a Program node.
    if (this.block.type === AST_NODE_TYPES.Program) {
      return true;
    }

    const bodyStart = this.block.body?.range[0] ?? -1;

    // It's invalid resolution in the following case:
    return !(
      (
        variable.scope === this &&
        ref.identifier.range[0] < bodyStart && // the reference is in the parameter part.
        variable.defs.every(d => d.name.range[0] >= bodyStart)
      ) // the variable is in the body.
    );
  }
}
```
</details>

#### Methods

##### `isValidResolution(ref: Reference, variable: Variable): boolean`

<details><summary>Code</summary>

```ts
protected override isValidResolution(
    ref: Reference,
    variable: Variable,
  ): boolean {
    // If `options.globalReturn` is true, `this.block` becomes a Program node.
    if (this.block.type === AST_NODE_TYPES.Program) {
      return true;
    }

    const bodyStart = this.block.body?.range[0] ?? -1;

    // It's invalid resolution in the following case:
    return !(
      (
        variable.scope === this &&
        ref.identifier.range[0] < bodyStart && // the reference is in the parameter part.
        variable.defs.every(d => d.name.range[0] >= bodyStart)
      ) // the variable is in the body.
    );
  }
```
</details>


---