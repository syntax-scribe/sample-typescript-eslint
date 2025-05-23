[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `ScopeManager.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 29
- **Classes**: 1
- **Imports**: 24
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/ScopeManager.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `SourceType` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `Scope` | `./scope` |
| `Variable` | `./variable` |
| `assert` | `./assert` |
| `BlockScope` | `./scope` |
| `CatchScope` | `./scope` |
| `ClassScope` | `./scope` |
| `ConditionalTypeScope` | `./scope` |
| `ForScope` | `./scope` |
| `FunctionExpressionNameScope` | `./scope` |
| `FunctionScope` | `./scope` |
| `FunctionTypeScope` | `./scope` |
| `GlobalScope` | `./scope` |
| `MappedTypeScope` | `./scope` |
| `ModuleScope` | `./scope` |
| `ScopeType` | `./scope` |
| `SwitchScope` | `./scope` |
| `TSEnumScope` | `./scope` |
| `TSModuleScope` | `./scope` |
| `TypeScope` | `./scope` |
| `WithScope` | `./scope` |
| `ClassFieldInitializerScope` | `./scope/ClassFieldInitializerScope` |
| `ClassStaticBlockScope` | `./scope/ClassStaticBlockScope` |


---

## Functions

### `ScopeManager.isES6(): boolean`

<details><summary>Code</summary>

```ts
public isES6(): boolean {
    return true;
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeManager.isGlobalReturn(): boolean`

<details><summary>Code</summary>

```ts
public isGlobalReturn(): boolean {
    return this.#options.globalReturn === true;
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeManager.isImpliedStrict(): boolean`

<details><summary>Code</summary>

```ts
public isImpliedStrict(): boolean {
    return this.#options.impliedStrict === true;
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeManager.isModule(): boolean`

<details><summary>Code</summary>

```ts
public isModule(): boolean {
    return this.#options.sourceType === 'module';
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeManager.isStrictModeSupported(): boolean`

<details><summary>Code</summary>

```ts
public isStrictModeSupported(): boolean {
    return true;
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeManager.getDeclaredVariables(node: TSESTree.Node): Variable[]`

<details><summary>Code</summary>

```ts
public getDeclaredVariables(node: TSESTree.Node): Variable[] {
    return this.declaredVariables.get(node) ?? [];
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Get the variables that a given AST node defines. The gotten variables' `def[].node`/`def[].parent` property is the node.
   * If the node does not define any variable, this returns an empty array.
   * @param node An AST node to get their variables.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `Variable[]`
- **Calls**:
  - `this.declaredVariables.get`
### `ScopeManager.acquire(node: TSESTree.Node, inner: boolean): Scope | null`

<details><summary>Code</summary>

```ts
public acquire(node: TSESTree.Node, inner = false): Scope | null {
    function predicate(testScope: Scope): boolean {
      if (
        testScope.type === ScopeType.function &&
        testScope.functionExpressionScope
      ) {
        return false;
      }
      return true;
    }

    const scopes = this.nodeToScope.get(node);

    if (!scopes || scopes.length === 0) {
      return null;
    }

    // Heuristic selection from all scopes.
    // If you would like to get all scopes, please use ScopeManager#acquireAll.
    if (scopes.length === 1) {
      return scopes[0];
    }

    if (inner) {
      for (let i = scopes.length - 1; i >= 0; --i) {
        const scope = scopes[i];

        if (predicate(scope)) {
          return scope;
        }
      }
      return null;
    }
    return scopes.find(predicate) ?? null;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Get the scope of a given AST node. The gotten scope's `block` property is the node.
   * This method never returns `function-expression-name` scope. If the node does not have their scope, this returns `null`.
   *
   * @param node An AST node to get their scope.
   * @param inner If the node has multiple scopes, this returns the outermost scope normally.
   *                If `inner` is `true` then this returns the innermost scope.
   */
```

- **Parameters**:
  - `node: TSESTree.Node`
  - `inner: boolean`
- **Return Type**: `Scope | null`
- **Calls**:
  - `this.nodeToScope.get`
  - `predicate`
  - `scopes.find`
- **Internal Comments**:
```
// Heuristic selection from all scopes.
// If you would like to get all scopes, please use ScopeManager#acquireAll.
```

### `ScopeManager.nestBlockScope(node: BlockScope['block']): BlockScope`

<details><summary>Code</summary>

```ts
public nestBlockScope(node: BlockScope['block']): BlockScope {
    assert(this.currentScope);
    return this.nestScope(new BlockScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: BlockScope['block']`
- **Return Type**: `BlockScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestCatchScope(node: CatchScope['block']): CatchScope`

<details><summary>Code</summary>

```ts
public nestCatchScope(node: CatchScope['block']): CatchScope {
    assert(this.currentScope);
    return this.nestScope(new CatchScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: CatchScope['block']`
- **Return Type**: `CatchScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestClassFieldInitializerScope(node: ClassFieldInitializerScope['block']): ClassFieldInitializerScope`

<details><summary>Code</summary>

```ts
public nestClassFieldInitializerScope(
    node: ClassFieldInitializerScope['block'],
  ): ClassFieldInitializerScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassFieldInitializerScope(this, this.currentScope, node),
    );
  }
```
</details>

- **Parameters**:
  - `node: ClassFieldInitializerScope['block']`
- **Return Type**: `ClassFieldInitializerScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestClassScope(node: ClassScope['block']): ClassScope`

<details><summary>Code</summary>

```ts
public nestClassScope(node: ClassScope['block']): ClassScope {
    assert(this.currentScope);
    return this.nestScope(new ClassScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: ClassScope['block']`
- **Return Type**: `ClassScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestClassStaticBlockScope(node: ClassStaticBlockScope['block']): ClassStaticBlockScope`

<details><summary>Code</summary>

```ts
public nestClassStaticBlockScope(
    node: ClassStaticBlockScope['block'],
  ): ClassStaticBlockScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassStaticBlockScope(this, this.currentScope, node),
    );
  }
```
</details>

- **Parameters**:
  - `node: ClassStaticBlockScope['block']`
- **Return Type**: `ClassStaticBlockScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestConditionalTypeScope(node: ConditionalTypeScope['block']): ConditionalTypeScope`

<details><summary>Code</summary>

```ts
public nestConditionalTypeScope(
    node: ConditionalTypeScope['block'],
  ): ConditionalTypeScope {
    assert(this.currentScope);
    return this.nestScope(
      new ConditionalTypeScope(this, this.currentScope, node),
    );
  }
```
</details>

- **Parameters**:
  - `node: ConditionalTypeScope['block']`
- **Return Type**: `ConditionalTypeScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestForScope(node: ForScope['block']): ForScope`

<details><summary>Code</summary>

```ts
public nestForScope(node: ForScope['block']): ForScope {
    assert(this.currentScope);
    return this.nestScope(new ForScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: ForScope['block']`
- **Return Type**: `ForScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestFunctionExpressionNameScope(node: FunctionExpressionNameScope['block']): FunctionExpressionNameScope`

<details><summary>Code</summary>

```ts
public nestFunctionExpressionNameScope(
    node: FunctionExpressionNameScope['block'],
  ): FunctionExpressionNameScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionExpressionNameScope(this, this.currentScope, node),
    );
  }
```
</details>

- **Parameters**:
  - `node: FunctionExpressionNameScope['block']`
- **Return Type**: `FunctionExpressionNameScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestFunctionScope(node: FunctionScope['block'], isMethodDefinition: boolean): FunctionScope`

<details><summary>Code</summary>

```ts
public nestFunctionScope(
    node: FunctionScope['block'],
    isMethodDefinition: boolean,
  ): FunctionScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionScope(this, this.currentScope, node, isMethodDefinition),
    );
  }
```
</details>

- **Parameters**:
  - `node: FunctionScope['block']`
  - `isMethodDefinition: boolean`
- **Return Type**: `FunctionScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestFunctionTypeScope(node: FunctionTypeScope['block']): FunctionTypeScope`

<details><summary>Code</summary>

```ts
public nestFunctionTypeScope(
    node: FunctionTypeScope['block'],
  ): FunctionTypeScope {
    assert(this.currentScope);
    return this.nestScope(new FunctionTypeScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: FunctionTypeScope['block']`
- **Return Type**: `FunctionTypeScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestGlobalScope(node: GlobalScope['block']): GlobalScope`

<details><summary>Code</summary>

```ts
public nestGlobalScope(node: GlobalScope['block']): GlobalScope {
    return this.nestScope(new GlobalScope(this, node));
  }
```
</details>

- **Parameters**:
  - `node: GlobalScope['block']`
- **Return Type**: `GlobalScope`
- **Calls**:
  - `this.nestScope`
### `ScopeManager.nestMappedTypeScope(node: MappedTypeScope['block']): MappedTypeScope`

<details><summary>Code</summary>

```ts
public nestMappedTypeScope(node: MappedTypeScope['block']): MappedTypeScope {
    assert(this.currentScope);
    return this.nestScope(new MappedTypeScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: MappedTypeScope['block']`
- **Return Type**: `MappedTypeScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestModuleScope(node: ModuleScope['block']): ModuleScope`

<details><summary>Code</summary>

```ts
public nestModuleScope(node: ModuleScope['block']): ModuleScope {
    assert(this.currentScope);
    return this.nestScope(new ModuleScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: ModuleScope['block']`
- **Return Type**: `ModuleScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestSwitchScope(node: SwitchScope['block']): SwitchScope`

<details><summary>Code</summary>

```ts
public nestSwitchScope(node: SwitchScope['block']): SwitchScope {
    assert(this.currentScope);
    return this.nestScope(new SwitchScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: SwitchScope['block']`
- **Return Type**: `SwitchScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestTSEnumScope(node: TSEnumScope['block']): TSEnumScope`

<details><summary>Code</summary>

```ts
public nestTSEnumScope(node: TSEnumScope['block']): TSEnumScope {
    assert(this.currentScope);
    return this.nestScope(new TSEnumScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: TSEnumScope['block']`
- **Return Type**: `TSEnumScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestTSModuleScope(node: TSModuleScope['block']): TSModuleScope`

<details><summary>Code</summary>

```ts
public nestTSModuleScope(node: TSModuleScope['block']): TSModuleScope {
    assert(this.currentScope);
    return this.nestScope(new TSModuleScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: TSModuleScope['block']`
- **Return Type**: `TSModuleScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestTypeScope(node: TypeScope['block']): TypeScope`

<details><summary>Code</summary>

```ts
public nestTypeScope(node: TypeScope['block']): TypeScope {
    assert(this.currentScope);
    return this.nestScope(new TypeScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: TypeScope['block']`
- **Return Type**: `TypeScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestWithScope(node: WithScope['block']): WithScope`

<details><summary>Code</summary>

```ts
public nestWithScope(node: WithScope['block']): WithScope {
    assert(this.currentScope);
    return this.nestScope(new WithScope(this, this.currentScope, node));
  }
```
</details>

- **Parameters**:
  - `node: WithScope['block']`
- **Return Type**: `WithScope`
- **Calls**:
  - `assert (from ./assert)`
  - `this.nestScope`
### `ScopeManager.nestScope(scope: T): T`

<details><summary>Code</summary>

```ts
protected nestScope<T extends Scope>(scope: T): T;
```
</details>

- **Parameters**:
  - `scope: T`
- **Return Type**: `T`
### `ScopeManager.nestScope(scope: Scope): Scope`

<details><summary>Code</summary>

```ts
protected nestScope(scope: Scope): Scope {
    if (scope instanceof GlobalScope) {
      assert(this.currentScope == null);
      this.globalScope = scope;
    }
    this.currentScope = scope;
    return scope;
  }
```
</details>

- **Parameters**:
  - `scope: Scope`
- **Return Type**: `Scope`
- **Calls**:
  - `assert (from ./assert)`
### `recurse(scope: Scope): void`

<details><summary>Code</summary>

```ts
function recurse(scope: Scope): void {
      scope.variables.forEach(v => variables.add(v));
      scope.childScopes.forEach(recurse);
    }
```
</details>

- **Parameters**:
  - `scope: Scope`
- **Return Type**: `void`
- **Calls**:
  - `scope.variables.forEach`
  - `variables.add`
  - `scope.childScopes.forEach`
### `predicate(testScope: Scope): boolean`

<details><summary>Code</summary>

```ts
function predicate(testScope: Scope): boolean {
      if (
        testScope.type === ScopeType.function &&
        testScope.functionExpressionScope
      ) {
        return false;
      }
      return true;
    }
```
</details>

- **Parameters**:
  - `testScope: Scope`
- **Return Type**: `boolean`

---

## Classes

### `ScopeManager`

<details><summary>Class Code</summary>

```ts
export class ScopeManager {
  readonly #options: ScopeManagerOptions;

  public currentScope: Scope | null;

  public readonly declaredVariables: WeakMap<TSESTree.Node, Variable[]>;

  /**
   * The root scope
   */
  public globalScope: GlobalScope | null;

  public readonly nodeToScope: WeakMap<TSESTree.Node, Scope[]>;

  /**
   * All scopes
   * @public
   */
  public readonly scopes: Scope[];

  constructor(options: ScopeManagerOptions) {
    this.scopes = [];
    this.globalScope = null;
    this.nodeToScope = new WeakMap();
    this.currentScope = null;
    this.#options = options;
    this.declaredVariables = new WeakMap();
  }

  public isES6(): boolean {
    return true;
  }

  public isGlobalReturn(): boolean {
    return this.#options.globalReturn === true;
  }

  public isImpliedStrict(): boolean {
    return this.#options.impliedStrict === true;
  }

  public isModule(): boolean {
    return this.#options.sourceType === 'module';
  }

  public isStrictModeSupported(): boolean {
    return true;
  }

  public get variables(): Variable[] {
    const variables = new Set<Variable>();
    function recurse(scope: Scope): void {
      scope.variables.forEach(v => variables.add(v));
      scope.childScopes.forEach(recurse);
    }
    this.scopes.forEach(recurse);
    return [...variables].sort((a, b) => a.$id - b.$id);
  }

  /**
   * Get the variables that a given AST node defines. The gotten variables' `def[].node`/`def[].parent` property is the node.
   * If the node does not define any variable, this returns an empty array.
   * @param node An AST node to get their variables.
   */
  public getDeclaredVariables(node: TSESTree.Node): Variable[] {
    return this.declaredVariables.get(node) ?? [];
  }

  /**
   * Get the scope of a given AST node. The gotten scope's `block` property is the node.
   * This method never returns `function-expression-name` scope. If the node does not have their scope, this returns `null`.
   *
   * @param node An AST node to get their scope.
   * @param inner If the node has multiple scopes, this returns the outermost scope normally.
   *                If `inner` is `true` then this returns the innermost scope.
   */
  public acquire(node: TSESTree.Node, inner = false): Scope | null {
    function predicate(testScope: Scope): boolean {
      if (
        testScope.type === ScopeType.function &&
        testScope.functionExpressionScope
      ) {
        return false;
      }
      return true;
    }

    const scopes = this.nodeToScope.get(node);

    if (!scopes || scopes.length === 0) {
      return null;
    }

    // Heuristic selection from all scopes.
    // If you would like to get all scopes, please use ScopeManager#acquireAll.
    if (scopes.length === 1) {
      return scopes[0];
    }

    if (inner) {
      for (let i = scopes.length - 1; i >= 0; --i) {
        const scope = scopes[i];

        if (predicate(scope)) {
          return scope;
        }
      }
      return null;
    }
    return scopes.find(predicate) ?? null;
  }

  public nestBlockScope(node: BlockScope['block']): BlockScope {
    assert(this.currentScope);
    return this.nestScope(new BlockScope(this, this.currentScope, node));
  }

  public nestCatchScope(node: CatchScope['block']): CatchScope {
    assert(this.currentScope);
    return this.nestScope(new CatchScope(this, this.currentScope, node));
  }

  public nestClassFieldInitializerScope(
    node: ClassFieldInitializerScope['block'],
  ): ClassFieldInitializerScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassFieldInitializerScope(this, this.currentScope, node),
    );
  }

  public nestClassScope(node: ClassScope['block']): ClassScope {
    assert(this.currentScope);
    return this.nestScope(new ClassScope(this, this.currentScope, node));
  }

  public nestClassStaticBlockScope(
    node: ClassStaticBlockScope['block'],
  ): ClassStaticBlockScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassStaticBlockScope(this, this.currentScope, node),
    );
  }

  public nestConditionalTypeScope(
    node: ConditionalTypeScope['block'],
  ): ConditionalTypeScope {
    assert(this.currentScope);
    return this.nestScope(
      new ConditionalTypeScope(this, this.currentScope, node),
    );
  }

  public nestForScope(node: ForScope['block']): ForScope {
    assert(this.currentScope);
    return this.nestScope(new ForScope(this, this.currentScope, node));
  }

  public nestFunctionExpressionNameScope(
    node: FunctionExpressionNameScope['block'],
  ): FunctionExpressionNameScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionExpressionNameScope(this, this.currentScope, node),
    );
  }

  public nestFunctionScope(
    node: FunctionScope['block'],
    isMethodDefinition: boolean,
  ): FunctionScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionScope(this, this.currentScope, node, isMethodDefinition),
    );
  }

  public nestFunctionTypeScope(
    node: FunctionTypeScope['block'],
  ): FunctionTypeScope {
    assert(this.currentScope);
    return this.nestScope(new FunctionTypeScope(this, this.currentScope, node));
  }

  public nestGlobalScope(node: GlobalScope['block']): GlobalScope {
    return this.nestScope(new GlobalScope(this, node));
  }

  public nestMappedTypeScope(node: MappedTypeScope['block']): MappedTypeScope {
    assert(this.currentScope);
    return this.nestScope(new MappedTypeScope(this, this.currentScope, node));
  }

  public nestModuleScope(node: ModuleScope['block']): ModuleScope {
    assert(this.currentScope);
    return this.nestScope(new ModuleScope(this, this.currentScope, node));
  }

  public nestSwitchScope(node: SwitchScope['block']): SwitchScope {
    assert(this.currentScope);
    return this.nestScope(new SwitchScope(this, this.currentScope, node));
  }

  public nestTSEnumScope(node: TSEnumScope['block']): TSEnumScope {
    assert(this.currentScope);
    return this.nestScope(new TSEnumScope(this, this.currentScope, node));
  }

  public nestTSModuleScope(node: TSModuleScope['block']): TSModuleScope {
    assert(this.currentScope);
    return this.nestScope(new TSModuleScope(this, this.currentScope, node));
  }

  public nestTypeScope(node: TypeScope['block']): TypeScope {
    assert(this.currentScope);
    return this.nestScope(new TypeScope(this, this.currentScope, node));
  }

  public nestWithScope(node: WithScope['block']): WithScope {
    assert(this.currentScope);
    return this.nestScope(new WithScope(this, this.currentScope, node));
  }

  // Scope helpers

  protected nestScope<T extends Scope>(scope: T): T;
  protected nestScope(scope: Scope): Scope {
    if (scope instanceof GlobalScope) {
      assert(this.currentScope == null);
      this.globalScope = scope;
    }
    this.currentScope = scope;
    return scope;
  }
}
```
</details>

#### Methods

##### `isES6(): boolean`

<details><summary>Code</summary>

```ts
public isES6(): boolean {
    return true;
  }
```
</details>

##### `isGlobalReturn(): boolean`

<details><summary>Code</summary>

```ts
public isGlobalReturn(): boolean {
    return this.#options.globalReturn === true;
  }
```
</details>

##### `isImpliedStrict(): boolean`

<details><summary>Code</summary>

```ts
public isImpliedStrict(): boolean {
    return this.#options.impliedStrict === true;
  }
```
</details>

##### `isModule(): boolean`

<details><summary>Code</summary>

```ts
public isModule(): boolean {
    return this.#options.sourceType === 'module';
  }
```
</details>

##### `isStrictModeSupported(): boolean`

<details><summary>Code</summary>

```ts
public isStrictModeSupported(): boolean {
    return true;
  }
```
</details>

##### `getDeclaredVariables(node: TSESTree.Node): Variable[]`

<details><summary>Code</summary>

```ts
public getDeclaredVariables(node: TSESTree.Node): Variable[] {
    return this.declaredVariables.get(node) ?? [];
  }
```
</details>

##### `acquire(node: TSESTree.Node, inner: boolean): Scope | null`

<details><summary>Code</summary>

```ts
public acquire(node: TSESTree.Node, inner = false): Scope | null {
    function predicate(testScope: Scope): boolean {
      if (
        testScope.type === ScopeType.function &&
        testScope.functionExpressionScope
      ) {
        return false;
      }
      return true;
    }

    const scopes = this.nodeToScope.get(node);

    if (!scopes || scopes.length === 0) {
      return null;
    }

    // Heuristic selection from all scopes.
    // If you would like to get all scopes, please use ScopeManager#acquireAll.
    if (scopes.length === 1) {
      return scopes[0];
    }

    if (inner) {
      for (let i = scopes.length - 1; i >= 0; --i) {
        const scope = scopes[i];

        if (predicate(scope)) {
          return scope;
        }
      }
      return null;
    }
    return scopes.find(predicate) ?? null;
  }
```
</details>

##### `nestBlockScope(node: BlockScope['block']): BlockScope`

<details><summary>Code</summary>

```ts
public nestBlockScope(node: BlockScope['block']): BlockScope {
    assert(this.currentScope);
    return this.nestScope(new BlockScope(this, this.currentScope, node));
  }
```
</details>

##### `nestCatchScope(node: CatchScope['block']): CatchScope`

<details><summary>Code</summary>

```ts
public nestCatchScope(node: CatchScope['block']): CatchScope {
    assert(this.currentScope);
    return this.nestScope(new CatchScope(this, this.currentScope, node));
  }
```
</details>

##### `nestClassFieldInitializerScope(node: ClassFieldInitializerScope['block']): ClassFieldInitializerScope`

<details><summary>Code</summary>

```ts
public nestClassFieldInitializerScope(
    node: ClassFieldInitializerScope['block'],
  ): ClassFieldInitializerScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassFieldInitializerScope(this, this.currentScope, node),
    );
  }
```
</details>

##### `nestClassScope(node: ClassScope['block']): ClassScope`

<details><summary>Code</summary>

```ts
public nestClassScope(node: ClassScope['block']): ClassScope {
    assert(this.currentScope);
    return this.nestScope(new ClassScope(this, this.currentScope, node));
  }
```
</details>

##### `nestClassStaticBlockScope(node: ClassStaticBlockScope['block']): ClassStaticBlockScope`

<details><summary>Code</summary>

```ts
public nestClassStaticBlockScope(
    node: ClassStaticBlockScope['block'],
  ): ClassStaticBlockScope {
    assert(this.currentScope);
    return this.nestScope(
      new ClassStaticBlockScope(this, this.currentScope, node),
    );
  }
```
</details>

##### `nestConditionalTypeScope(node: ConditionalTypeScope['block']): ConditionalTypeScope`

<details><summary>Code</summary>

```ts
public nestConditionalTypeScope(
    node: ConditionalTypeScope['block'],
  ): ConditionalTypeScope {
    assert(this.currentScope);
    return this.nestScope(
      new ConditionalTypeScope(this, this.currentScope, node),
    );
  }
```
</details>

##### `nestForScope(node: ForScope['block']): ForScope`

<details><summary>Code</summary>

```ts
public nestForScope(node: ForScope['block']): ForScope {
    assert(this.currentScope);
    return this.nestScope(new ForScope(this, this.currentScope, node));
  }
```
</details>

##### `nestFunctionExpressionNameScope(node: FunctionExpressionNameScope['block']): FunctionExpressionNameScope`

<details><summary>Code</summary>

```ts
public nestFunctionExpressionNameScope(
    node: FunctionExpressionNameScope['block'],
  ): FunctionExpressionNameScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionExpressionNameScope(this, this.currentScope, node),
    );
  }
```
</details>

##### `nestFunctionScope(node: FunctionScope['block'], isMethodDefinition: boolean): FunctionScope`

<details><summary>Code</summary>

```ts
public nestFunctionScope(
    node: FunctionScope['block'],
    isMethodDefinition: boolean,
  ): FunctionScope {
    assert(this.currentScope);
    return this.nestScope(
      new FunctionScope(this, this.currentScope, node, isMethodDefinition),
    );
  }
```
</details>

##### `nestFunctionTypeScope(node: FunctionTypeScope['block']): FunctionTypeScope`

<details><summary>Code</summary>

```ts
public nestFunctionTypeScope(
    node: FunctionTypeScope['block'],
  ): FunctionTypeScope {
    assert(this.currentScope);
    return this.nestScope(new FunctionTypeScope(this, this.currentScope, node));
  }
```
</details>

##### `nestGlobalScope(node: GlobalScope['block']): GlobalScope`

<details><summary>Code</summary>

```ts
public nestGlobalScope(node: GlobalScope['block']): GlobalScope {
    return this.nestScope(new GlobalScope(this, node));
  }
```
</details>

##### `nestMappedTypeScope(node: MappedTypeScope['block']): MappedTypeScope`

<details><summary>Code</summary>

```ts
public nestMappedTypeScope(node: MappedTypeScope['block']): MappedTypeScope {
    assert(this.currentScope);
    return this.nestScope(new MappedTypeScope(this, this.currentScope, node));
  }
```
</details>

##### `nestModuleScope(node: ModuleScope['block']): ModuleScope`

<details><summary>Code</summary>

```ts
public nestModuleScope(node: ModuleScope['block']): ModuleScope {
    assert(this.currentScope);
    return this.nestScope(new ModuleScope(this, this.currentScope, node));
  }
```
</details>

##### `nestSwitchScope(node: SwitchScope['block']): SwitchScope`

<details><summary>Code</summary>

```ts
public nestSwitchScope(node: SwitchScope['block']): SwitchScope {
    assert(this.currentScope);
    return this.nestScope(new SwitchScope(this, this.currentScope, node));
  }
```
</details>

##### `nestTSEnumScope(node: TSEnumScope['block']): TSEnumScope`

<details><summary>Code</summary>

```ts
public nestTSEnumScope(node: TSEnumScope['block']): TSEnumScope {
    assert(this.currentScope);
    return this.nestScope(new TSEnumScope(this, this.currentScope, node));
  }
```
</details>

##### `nestTSModuleScope(node: TSModuleScope['block']): TSModuleScope`

<details><summary>Code</summary>

```ts
public nestTSModuleScope(node: TSModuleScope['block']): TSModuleScope {
    assert(this.currentScope);
    return this.nestScope(new TSModuleScope(this, this.currentScope, node));
  }
```
</details>

##### `nestTypeScope(node: TypeScope['block']): TypeScope`

<details><summary>Code</summary>

```ts
public nestTypeScope(node: TypeScope['block']): TypeScope {
    assert(this.currentScope);
    return this.nestScope(new TypeScope(this, this.currentScope, node));
  }
```
</details>

##### `nestWithScope(node: WithScope['block']): WithScope`

<details><summary>Code</summary>

```ts
public nestWithScope(node: WithScope['block']): WithScope {
    assert(this.currentScope);
    return this.nestScope(new WithScope(this, this.currentScope, node));
  }
```
</details>

##### `nestScope(scope: T): T`

<details><summary>Code</summary>

```ts
protected nestScope<T extends Scope>(scope: T): T;
```
</details>

##### `nestScope(scope: Scope): Scope`

<details><summary>Code</summary>

```ts
protected nestScope(scope: Scope): Scope {
    if (scope instanceof GlobalScope) {
      assert(this.currentScope == null);
      this.globalScope = scope;
    }
    this.currentScope = scope;
    return scope;
  }
```
</details>


---

## Interfaces

### `ScopeManagerOptions`

<details><summary>Interface Code</summary>

```ts
interface ScopeManagerOptions {
  globalReturn?: boolean;
  impliedStrict?: boolean;
  sourceType?: SourceType;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `globalReturn` | `boolean` | ✓ |  |
| `impliedStrict` | `boolean` | ✓ |  |
| `sourceType` | `SourceType` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---