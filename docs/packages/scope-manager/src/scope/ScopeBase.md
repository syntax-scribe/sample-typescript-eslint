[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ScopeBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 16 |
| 🧱 Classes | 1 |
| 📦 Imports | 18 |
| 📊 Variables & Constants | 16 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/scope/ScopeBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Definition` | `../definition` |
| `ReferenceImplicitGlobal` | `../referencer/Reference` |
| `ScopeManager` | `../ScopeManager` |
| `FunctionScope` | `./FunctionScope` |
| `GlobalScope` | `./GlobalScope` |
| `ModuleScope` | `./ModuleScope` |
| `Scope` | `./Scope` |
| `TSModuleScope` | `./TSModuleScope` |
| `assert` | `../assert` |
| `DefinitionType` | `../definition` |
| `createIdGenerator` | `../ID` |
| `Reference` | `../referencer/Reference` |
| `ReferenceFlag` | `../referencer/Reference` |
| `ReferenceTypeFlag` | `../referencer/Reference` |
| `Variable` | `../variable` |
| `ScopeType` | `./ScopeType` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `body` | `TSESTree.BlockStatement | TSESTree.Program | null | undefined` | let/var | `*not shown*` | ✗ |
| `functionBody` | `any` | const | `block as FunctionScope['block']` | ✗ |
| `expr` | `any` | const | `stmt.expression` | ✗ |
| `VARIABLE_SCOPE_TYPES` | `Set<ScopeType>` | const | `new Set([
  ScopeType.classFieldInitializer,
  ScopeType.classStaticBlock,
  ScopeType.function,
  ScopeType.global,
  ScopeType.module,
  ScopeType.tsModule,
])` | ✗ |
| `current` | `Scope` | let/var | `this as Scope | null` | ✗ |
| `name` | `any` | const | `ref.identifier.name` | ✗ |
| `isValidTypeReference` | `boolean` | const | `ref.isTypeReference && variable.isTypeVariable` | ✗ |
| `isValidValueReference` | `boolean` | const | `ref.isValueReference && variable.isValueVariable` | ✗ |
| `upperScopeAsScopeBase` | `Upper` | const | `upperScope` | ✗ |
| `name` | `any` | const | `ref.identifier.name` | ✗ |
| `defs` | `Definition[]` | const | `variable.defs` | ✗ |
| `closeRef` | `(ref: Reference, scopeManager: ScopeManager) => void` | let/var | `*not shown*` | ✗ |
| `name` | `string` | const | `typeof nameOrVariable === 'string' ? nameOrVariable : nameOrVariable.name` | ✗ |
| `ref` | `Reference` | const | `new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type | ReferenceTypeFlag.Value,
    )` | ✗ |
| `ref` | `Reference` | const | `new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type,
    )` | ✗ |
| `ref` | `Reference` | const | `new Reference(
      node,
      this as Scope,
      assign,
      writeExpr,
      maybeImplicitGlobal,
      init,
      ReferenceTypeFlag.Value,
    )` | ✗ |


---

## Functions

### `isStrictScope(scope: Scope, block: TSESTree.Node, isMethodDefinition: boolean): boolean`

<details><summary>Code</summary>

```ts
function isStrictScope(
  scope: Scope,
  block: TSESTree.Node,
  isMethodDefinition: boolean,
): boolean {
  let body: TSESTree.BlockStatement | TSESTree.Program | null | undefined;

  // When upper scope is exists and strict, inner scope is also strict.
  if (scope.upper?.isStrict) {
    return true;
  }

  if (isMethodDefinition) {
    return true;
  }

  if (
    scope.type === ScopeType.class ||
    scope.type === ScopeType.conditionalType ||
    scope.type === ScopeType.functionType ||
    scope.type === ScopeType.mappedType ||
    scope.type === ScopeType.module ||
    scope.type === ScopeType.tsEnum ||
    scope.type === ScopeType.tsModule ||
    scope.type === ScopeType.type
  ) {
    return true;
  }

  if (scope.type === ScopeType.block || scope.type === ScopeType.switch) {
    return false;
  }

  if (scope.type === ScopeType.function) {
    const functionBody = block as FunctionScope['block'];
    switch (functionBody.type) {
      case AST_NODE_TYPES.ArrowFunctionExpression:
        if (functionBody.body.type !== AST_NODE_TYPES.BlockStatement) {
          return false;
        }
        body = functionBody.body;
        break;

      case AST_NODE_TYPES.Program:
        body = functionBody;
        break;

      default:
        body = functionBody.body;
    }

    if (!body) {
      return false;
    }
  } else if (scope.type === ScopeType.global) {
    body = block as GlobalScope['block'];
  } else {
    return false;
  }

  // Search 'use strict' directive.
  for (const stmt of body.body) {
    if (stmt.type !== AST_NODE_TYPES.ExpressionStatement) {
      break;
    }

    if (stmt.directive === 'use strict') {
      return true;
    }

    const expr = stmt.expression;
    if (expr.type !== AST_NODE_TYPES.Literal) {
      break;
    }
    if (expr.raw === '"use strict"' || expr.raw === "'use strict'") {
      return true;
    }
    if (expr.value === 'use strict') {
      return true;
    }
  }
  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Test if scope is strict
 */
```

- **Parameters**:
  - `scope: Scope`
  - `block: TSESTree.Node`
  - `isMethodDefinition: boolean`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// When upper scope is exists and strict, inner scope is also strict.
// Search 'use strict' directive.
```

### `registerScope(scopeManager: ScopeManager, scope: Scope): void`

<details><summary>Code</summary>

```ts
function registerScope(scopeManager: ScopeManager, scope: Scope): void {
  scopeManager.scopes.push(scope);

  const scopes = scopeManager.nodeToScope.get(scope.block);

  if (scopes) {
    scopes.push(scope);
  } else {
    scopeManager.nodeToScope.set(scope.block, [scope]);
  }
}
```
</details>

- **Parameters**:
  - `scopeManager: ScopeManager`
  - `scope: Scope`
- **Return Type**: `void`
- **Calls**:
  - `scopeManager.scopes.push`
  - `scopeManager.nodeToScope.get`
  - `scopes.push`
  - `scopeManager.nodeToScope.set`
### `ScopeBase.isVariableScope(): this is VariableScope`

<details><summary>Code</summary>

```ts
private isVariableScope(): this is VariableScope {
    return VARIABLE_SCOPE_TYPES.has(this.type);
  }
```
</details>

- **Return Type**: `this is VariableScope`
- **Calls**:
  - `VARIABLE_SCOPE_TYPES.has`
### `ScopeBase.shouldStaticallyCloseForGlobal(ref: Reference, scopeManager: ScopeManager): boolean`

<details><summary>Code</summary>

```ts
private shouldStaticallyCloseForGlobal(
    ref: Reference,
    scopeManager: ScopeManager,
  ): boolean {
    // On global scope, let/const/class declarations should be resolved statically.
    const name = ref.identifier.name;

    const variable = this.set.get(name);
    if (!variable) {
      return false;
    }
    // variable exists on the scope

    // in module mode, we can statically resolve everything, regardless of its decl type
    if (scopeManager.isModule()) {
      return true;
    }

    // in script mode, only certain cases should be statically resolved
    // Example:
    // a `var` decl is ignored by the runtime if it clashes with a global name
    // this means that we should not resolve the reference to the variable
    const defs = variable.defs;
    return (
      defs.length > 0 &&
      defs.every(def => {
        if (def.type === DefinitionType.Variable && def.parent.kind === 'var') {
          return false;
        }
        return true;
      })
    );
  }
```
</details>

- **Parameters**:
  - `ref: Reference`
  - `scopeManager: ScopeManager`
- **Return Type**: `boolean`
- **Calls**:
  - `this.set.get`
  - `scopeManager.isModule`
  - `defs.every`
- **Internal Comments**:
```
// On global scope, let/const/class declarations should be resolved statically. (x2)
// variable exists on the scope
// in module mode, we can statically resolve everything, regardless of its decl type
// in script mode, only certain cases should be statically resolved (x2)
// Example: (x2)
// a `var` decl is ignored by the runtime if it clashes with a global name (x2)
// this means that we should not resolve the reference to the variable (x2)
```

### `ScopeBase.close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public close(scopeManager: ScopeManager): Scope | null {
    let closeRef: (ref: Reference, scopeManager: ScopeManager) => void;

    if (this.shouldStaticallyClose()) {
      closeRef = this.#staticCloseRef;
    } else if (this.type !== 'global') {
      closeRef = this.#dynamicCloseRef;
    } else {
      closeRef = this.#globalCloseRef;
    }

    // Try Resolving all references in this scope.
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => closeRef(ref, scopeManager));
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
  - `assert (from ../assert)`
  - `this.leftToResolve.forEach`
  - `closeRef`
- **Internal Comments**:
```
// Try Resolving all references in this scope. (x3)
```

### `ScopeBase.shouldStaticallyClose(): boolean`

<details><summary>Code</summary>

```ts
public shouldStaticallyClose(): boolean {
    return !this.#dynamic;
  }
```
</details>

- **Return Type**: `boolean`
### `ScopeBase.defineVariable(nameOrVariable: string | Variable, set: Map<string, Variable>, variables: Variable[], node: TSESTree.Identifier | null, def: Definition | null): void`

<details><summary>Code</summary>

```ts
protected defineVariable(
    nameOrVariable: string | Variable,
    set: Map<string, Variable>,
    variables: Variable[],
    node: TSESTree.Identifier | null,
    def: Definition | null,
  ): void {
    const name =
      typeof nameOrVariable === 'string' ? nameOrVariable : nameOrVariable.name;
    let variable = set.get(name);
    if (!variable) {
      variable =
        typeof nameOrVariable === 'string'
          ? new Variable(name, this as Scope)
          : nameOrVariable;
      set.set(name, variable);
      variables.push(variable);
    }

    if (def) {
      variable.defs.push(def);
      this.addDeclaredVariablesOfNode(variable, def.node);
      this.addDeclaredVariablesOfNode(variable, def.parent);
    }
    if (node) {
      variable.identifiers.push(node);
    }
  }
```
</details>

- **JSDoc**:
```ts
/**
   * To override by function scopes.
   * References in default parameters isn't resolved to variables which are in their function body.
   */
```

- **Parameters**:
  - `nameOrVariable: string | Variable`
  - `set: Map<string, Variable>`
  - `variables: Variable[]`
  - `node: TSESTree.Identifier | null`
  - `def: Definition | null`
- **Return Type**: `void`
- **Calls**:
  - `set.get`
  - `set.set`
  - `variables.push`
  - `variable.defs.push`
  - `this.addDeclaredVariablesOfNode`
  - `variable.identifiers.push`
### `ScopeBase.delegateToUpperScope(ref: Reference): void`

<details><summary>Code</summary>

```ts
protected delegateToUpperScope(ref: Reference): void {
    (this.upper as AnyScope | undefined)?.leftToResolve?.push(ref);
    this.through.push(ref);
  }
```
</details>

- **Parameters**:
  - `ref: Reference`
- **Return Type**: `void`
- **Calls**:
  - `(this.upper as AnyScope | undefined)?.leftToResolve?.push`
  - `this.through.push`
### `ScopeBase.isValidResolution(_ref: Reference, _variable: Variable): boolean`

<details><summary>Code</summary>

```ts
protected isValidResolution(_ref: Reference, _variable: Variable): boolean {
    return true;
  }
```
</details>

- **Parameters**:
  - `_ref: Reference`
  - `_variable: Variable`
- **Return Type**: `boolean`
### `ScopeBase.addDeclaredVariablesOfNode(variable: Variable, node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
private addDeclaredVariablesOfNode(
    variable: Variable,
    node: TSESTree.Node | null | undefined,
  ): void {
    if (node == null) {
      return;
    }

    let variables = this.#declaredVariables.get(node);

    if (variables == null) {
      variables = [];
      this.#declaredVariables.set(node, variables);
    }
    if (!variables.includes(variable)) {
      variables.push(variable);
    }
  }
```
</details>

- **Parameters**:
  - `variable: Variable`
  - `node: TSESTree.Node | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `this.#declaredVariables.get`
  - `this.#declaredVariables.set`
  - `variables.includes`
  - `variables.push`
### `ScopeBase.defineIdentifier(node: TSESTree.Identifier, def: Definition): void`

<details><summary>Code</summary>

```ts
public defineIdentifier(node: TSESTree.Identifier, def: Definition): void {
    this.defineVariable(node.name, this.set, this.variables, node, def);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
  - `def: Definition`
- **Return Type**: `void`
- **Calls**:
  - `this.defineVariable`
### `ScopeBase.defineLiteralIdentifier(node: TSESTree.StringLiteral, def: Definition): void`

<details><summary>Code</summary>

```ts
public defineLiteralIdentifier(
    node: TSESTree.StringLiteral,
    def: Definition,
  ): void {
    this.defineVariable(node.value, this.set, this.variables, null, def);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.StringLiteral`
  - `def: Definition`
- **Return Type**: `void`
- **Calls**:
  - `this.defineVariable`
### `ScopeBase.referenceDualValueType(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
public referenceDualValueType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type | ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.references.push`
  - `this.leftToResolve?.push`
### `ScopeBase.referenceType(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
public referenceType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.references.push`
  - `this.leftToResolve?.push`
### `ScopeBase.referenceValue(node: TSESTree.Identifier | TSESTree.JSXIdentifier, assign: ReferenceFlag, writeExpr: TSESTree.Expression | null, maybeImplicitGlobal: ReferenceImplicitGlobal | null, init: boolean): void`

<details><summary>Code</summary>

```ts
public referenceValue(
    node: TSESTree.Identifier | TSESTree.JSXIdentifier,
    assign: ReferenceFlag = ReferenceFlag.Read,
    writeExpr?: TSESTree.Expression | null,
    maybeImplicitGlobal?: ReferenceImplicitGlobal | null,
    init = false,
  ): void {
    const ref = new Reference(
      node,
      this as Scope,
      assign,
      writeExpr,
      maybeImplicitGlobal,
      init,
      ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier | TSESTree.JSXIdentifier`
  - `assign: ReferenceFlag`
  - `writeExpr: TSESTree.Expression | null`
  - `maybeImplicitGlobal: ReferenceImplicitGlobal | null`
  - `init: boolean`
- **Return Type**: `void`
- **Calls**:
  - `this.references.push`
  - `this.leftToResolve?.push`
### `resolve(): boolean`

<details><summary>Code</summary>

```ts
(): boolean => {
      const name = ref.identifier.name;
      const variable = this.set.get(name);

      if (!variable) {
        return false;
      }

      if (!this.isValidResolution(ref, variable)) {
        return false;
      }

      // make sure we don't match a type reference to a value variable
      const isValidTypeReference =
        ref.isTypeReference && variable.isTypeVariable;
      const isValidValueReference =
        ref.isValueReference && variable.isValueVariable;
      if (!isValidTypeReference && !isValidValueReference) {
        return false;
      }

      variable.references.push(ref);
      ref.resolved = variable;

      return true;
    }
```
</details>

- **Return Type**: `boolean`
- **Calls**:
  - `this.set.get`
  - `this.isValidResolution`
  - `variable.references.push`
- **Internal Comments**:
```
// make sure we don't match a type reference to a value variable (x2)
```


---

## Classes

### `ScopeBase`

<details><summary>Class Code</summary>

```ts
export abstract class ScopeBase<
  Type extends ScopeType,
  Block extends TSESTree.Node,
  Upper extends Scope | null,
> {
  /**
   * A unique ID for this instance - primarily used to help debugging and testing
   */
  public readonly $id: number = generator();

  /**
   * The AST node which created this scope.
   * @public
   */
  public readonly block: Block;
  /**
   * The array of child scopes. This does not include grandchild scopes.
   * @public
   */
  public readonly childScopes: Scope[] = [];
  /**
   * A map of the variables for each node in this scope.
   * This is map is a pointer to the one in the parent ScopeManager instance
   */
  readonly #declaredVariables: WeakMap<TSESTree.Node, Variable[]>;
  /**
   * Generally, through the lexical scoping of JS you can always know which variable an identifier in the source code
   * refers to. There are a few exceptions to this rule. With `global` and `with` scopes you can only decide at runtime
   * which variable a reference refers to.
   * All those scopes are considered "dynamic".
   */
  #dynamic: boolean;
  /**
   * Whether this scope is created by a FunctionExpression.
   * @public
   */
  public readonly functionExpressionScope: boolean = false;
  /**
   * Whether 'use strict' is in effect in this scope.
   * @public
   */
  public isStrict: boolean;
  /**
   * List of {@link Reference}s that are left to be resolved (i.e. which
   * need to be linked to the variable they refer to).
   */
  protected leftToResolve: Reference[] | null = [];
  /**
   * Any variable {@link Reference} found in this scope.
   * This includes occurrences of local variables as well as variables from parent scopes (including the global scope).
   * For local variables this also includes defining occurrences (like in a 'var' statement).
   * In a 'function' scope this does not include the occurrences of the formal parameter in the parameter list.
   * @public
   */
  public readonly references: Reference[] = [];
  /**
   * The map from variable names to variable objects.
   * @public
   */
  public readonly set = new Map<string, Variable>();
  /**
   * The {@link Reference}s that are not resolved with this scope.
   * @public
   */
  public readonly through: Reference[] = [];
  public readonly type: Type;
  /**
   * Reference to the parent {@link Scope}.
   * @public
   */
  public readonly upper: Upper;
  /**
   * The scoped {@link Variable}s of this scope.
   * In the case of a 'function' scope this includes the automatic argument `arguments` as its first element, as well
   * as all further formal arguments.
   * This does not include variables which are defined in child scopes.
   * @public
   */
  public readonly variables: Variable[] = [];
  /**
   * For scopes that can contain variable declarations, this is a self-reference.
   * For other scope types this is the *variableScope* value of the parent scope.
   * @public
   */
  #dynamicCloseRef = (ref: Reference): void => {
    // notify all names are through to global
    let current = this as Scope | null;

    do {
      /* eslint-disable @typescript-eslint/no-non-null-assertion */
      current!.through.push(ref);
      current = current!.upper;
      /* eslint-enable @typescript-eslint/no-non-null-assertion */
    } while (current);
  };

  #globalCloseRef = (ref: Reference, scopeManager: ScopeManager): void => {
    // let/const/class declarations should be resolved statically.
    // others should be resolved dynamically.
    if (this.shouldStaticallyCloseForGlobal(ref, scopeManager)) {
      this.#staticCloseRef(ref);
    } else {
      this.#dynamicCloseRef(ref);
    }
  };

  #staticCloseRef = (ref: Reference): void => {
    const resolve = (): boolean => {
      const name = ref.identifier.name;
      const variable = this.set.get(name);

      if (!variable) {
        return false;
      }

      if (!this.isValidResolution(ref, variable)) {
        return false;
      }

      // make sure we don't match a type reference to a value variable
      const isValidTypeReference =
        ref.isTypeReference && variable.isTypeVariable;
      const isValidValueReference =
        ref.isValueReference && variable.isValueVariable;
      if (!isValidTypeReference && !isValidValueReference) {
        return false;
      }

      variable.references.push(ref);
      ref.resolved = variable;

      return true;
    };

    if (!resolve()) {
      this.delegateToUpperScope(ref);
    }
  };

  public readonly variableScope: VariableScope;

  constructor(
    scopeManager: ScopeManager,
    type: Type,
    upperScope: Upper,
    block: Block,
    isMethodDefinition: boolean,
  ) {
    const upperScopeAsScopeBase = upperScope;

    this.type = type;
    this.#dynamic =
      this.type === ScopeType.global || this.type === ScopeType.with;
    this.block = block;
    this.variableScope = this.isVariableScope()
      ? this
      : // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
        upperScopeAsScopeBase!.variableScope;
    this.upper = upperScope;

    /**
     * Whether 'use strict' is in effect in this scope.
     * @member {boolean} Scope#isStrict
     */
    this.isStrict = isStrictScope(this as Scope, block, isMethodDefinition);

    // this is guaranteed to be correct at runtime
    upperScopeAsScopeBase?.childScopes.push(this as Scope);

    this.#declaredVariables = scopeManager.declaredVariables;

    registerScope(scopeManager, this as Scope);
  }

  private isVariableScope(): this is VariableScope {
    return VARIABLE_SCOPE_TYPES.has(this.type);
  }

  private shouldStaticallyCloseForGlobal(
    ref: Reference,
    scopeManager: ScopeManager,
  ): boolean {
    // On global scope, let/const/class declarations should be resolved statically.
    const name = ref.identifier.name;

    const variable = this.set.get(name);
    if (!variable) {
      return false;
    }
    // variable exists on the scope

    // in module mode, we can statically resolve everything, regardless of its decl type
    if (scopeManager.isModule()) {
      return true;
    }

    // in script mode, only certain cases should be statically resolved
    // Example:
    // a `var` decl is ignored by the runtime if it clashes with a global name
    // this means that we should not resolve the reference to the variable
    const defs = variable.defs;
    return (
      defs.length > 0 &&
      defs.every(def => {
        if (def.type === DefinitionType.Variable && def.parent.kind === 'var') {
          return false;
        }
        return true;
      })
    );
  }

  public close(scopeManager: ScopeManager): Scope | null {
    let closeRef: (ref: Reference, scopeManager: ScopeManager) => void;

    if (this.shouldStaticallyClose()) {
      closeRef = this.#staticCloseRef;
    } else if (this.type !== 'global') {
      closeRef = this.#dynamicCloseRef;
    } else {
      closeRef = this.#globalCloseRef;
    }

    // Try Resolving all references in this scope.
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => closeRef(ref, scopeManager));
    this.leftToResolve = null;

    return this.upper;
  }

  public shouldStaticallyClose(): boolean {
    return !this.#dynamic;
  }

  /**
   * To override by function scopes.
   * References in default parameters isn't resolved to variables which are in their function body.
   */
  protected defineVariable(
    nameOrVariable: string | Variable,
    set: Map<string, Variable>,
    variables: Variable[],
    node: TSESTree.Identifier | null,
    def: Definition | null,
  ): void {
    const name =
      typeof nameOrVariable === 'string' ? nameOrVariable : nameOrVariable.name;
    let variable = set.get(name);
    if (!variable) {
      variable =
        typeof nameOrVariable === 'string'
          ? new Variable(name, this as Scope)
          : nameOrVariable;
      set.set(name, variable);
      variables.push(variable);
    }

    if (def) {
      variable.defs.push(def);
      this.addDeclaredVariablesOfNode(variable, def.node);
      this.addDeclaredVariablesOfNode(variable, def.parent);
    }
    if (node) {
      variable.identifiers.push(node);
    }
  }

  protected delegateToUpperScope(ref: Reference): void {
    (this.upper as AnyScope | undefined)?.leftToResolve?.push(ref);
    this.through.push(ref);
  }

  protected isValidResolution(_ref: Reference, _variable: Variable): boolean {
    return true;
  }

  private addDeclaredVariablesOfNode(
    variable: Variable,
    node: TSESTree.Node | null | undefined,
  ): void {
    if (node == null) {
      return;
    }

    let variables = this.#declaredVariables.get(node);

    if (variables == null) {
      variables = [];
      this.#declaredVariables.set(node, variables);
    }
    if (!variables.includes(variable)) {
      variables.push(variable);
    }
  }

  public defineIdentifier(node: TSESTree.Identifier, def: Definition): void {
    this.defineVariable(node.name, this.set, this.variables, node, def);
  }

  public defineLiteralIdentifier(
    node: TSESTree.StringLiteral,
    def: Definition,
  ): void {
    this.defineVariable(node.value, this.set, this.variables, null, def);
  }

  public referenceDualValueType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type | ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }

  public referenceType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }

  public referenceValue(
    node: TSESTree.Identifier | TSESTree.JSXIdentifier,
    assign: ReferenceFlag = ReferenceFlag.Read,
    writeExpr?: TSESTree.Expression | null,
    maybeImplicitGlobal?: ReferenceImplicitGlobal | null,
    init = false,
  ): void {
    const ref = new Reference(
      node,
      this as Scope,
      assign,
      writeExpr,
      maybeImplicitGlobal,
      init,
      ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
}
```
</details>

#### Methods

##### `isVariableScope(): this is VariableScope`

<details><summary>Code</summary>

```ts
private isVariableScope(): this is VariableScope {
    return VARIABLE_SCOPE_TYPES.has(this.type);
  }
```
</details>

##### `shouldStaticallyCloseForGlobal(ref: Reference, scopeManager: ScopeManager): boolean`

<details><summary>Code</summary>

```ts
private shouldStaticallyCloseForGlobal(
    ref: Reference,
    scopeManager: ScopeManager,
  ): boolean {
    // On global scope, let/const/class declarations should be resolved statically.
    const name = ref.identifier.name;

    const variable = this.set.get(name);
    if (!variable) {
      return false;
    }
    // variable exists on the scope

    // in module mode, we can statically resolve everything, regardless of its decl type
    if (scopeManager.isModule()) {
      return true;
    }

    // in script mode, only certain cases should be statically resolved
    // Example:
    // a `var` decl is ignored by the runtime if it clashes with a global name
    // this means that we should not resolve the reference to the variable
    const defs = variable.defs;
    return (
      defs.length > 0 &&
      defs.every(def => {
        if (def.type === DefinitionType.Variable && def.parent.kind === 'var') {
          return false;
        }
        return true;
      })
    );
  }
```
</details>

##### `close(scopeManager: ScopeManager): Scope | null`

<details><summary>Code</summary>

```ts
public close(scopeManager: ScopeManager): Scope | null {
    let closeRef: (ref: Reference, scopeManager: ScopeManager) => void;

    if (this.shouldStaticallyClose()) {
      closeRef = this.#staticCloseRef;
    } else if (this.type !== 'global') {
      closeRef = this.#dynamicCloseRef;
    } else {
      closeRef = this.#globalCloseRef;
    }

    // Try Resolving all references in this scope.
    assert(this.leftToResolve);
    this.leftToResolve.forEach(ref => closeRef(ref, scopeManager));
    this.leftToResolve = null;

    return this.upper;
  }
```
</details>

##### `shouldStaticallyClose(): boolean`

<details><summary>Code</summary>

```ts
public shouldStaticallyClose(): boolean {
    return !this.#dynamic;
  }
```
</details>

##### `defineVariable(nameOrVariable: string | Variable, set: Map<string, Variable>, variables: Variable[], node: TSESTree.Identifier | null, def: Definition | null): void`

<details><summary>Code</summary>

```ts
protected defineVariable(
    nameOrVariable: string | Variable,
    set: Map<string, Variable>,
    variables: Variable[],
    node: TSESTree.Identifier | null,
    def: Definition | null,
  ): void {
    const name =
      typeof nameOrVariable === 'string' ? nameOrVariable : nameOrVariable.name;
    let variable = set.get(name);
    if (!variable) {
      variable =
        typeof nameOrVariable === 'string'
          ? new Variable(name, this as Scope)
          : nameOrVariable;
      set.set(name, variable);
      variables.push(variable);
    }

    if (def) {
      variable.defs.push(def);
      this.addDeclaredVariablesOfNode(variable, def.node);
      this.addDeclaredVariablesOfNode(variable, def.parent);
    }
    if (node) {
      variable.identifiers.push(node);
    }
  }
```
</details>

##### `delegateToUpperScope(ref: Reference): void`

<details><summary>Code</summary>

```ts
protected delegateToUpperScope(ref: Reference): void {
    (this.upper as AnyScope | undefined)?.leftToResolve?.push(ref);
    this.through.push(ref);
  }
```
</details>

##### `isValidResolution(_ref: Reference, _variable: Variable): boolean`

<details><summary>Code</summary>

```ts
protected isValidResolution(_ref: Reference, _variable: Variable): boolean {
    return true;
  }
```
</details>

##### `addDeclaredVariablesOfNode(variable: Variable, node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
private addDeclaredVariablesOfNode(
    variable: Variable,
    node: TSESTree.Node | null | undefined,
  ): void {
    if (node == null) {
      return;
    }

    let variables = this.#declaredVariables.get(node);

    if (variables == null) {
      variables = [];
      this.#declaredVariables.set(node, variables);
    }
    if (!variables.includes(variable)) {
      variables.push(variable);
    }
  }
```
</details>

##### `defineIdentifier(node: TSESTree.Identifier, def: Definition): void`

<details><summary>Code</summary>

```ts
public defineIdentifier(node: TSESTree.Identifier, def: Definition): void {
    this.defineVariable(node.name, this.set, this.variables, node, def);
  }
```
</details>

##### `defineLiteralIdentifier(node: TSESTree.StringLiteral, def: Definition): void`

<details><summary>Code</summary>

```ts
public defineLiteralIdentifier(
    node: TSESTree.StringLiteral,
    def: Definition,
  ): void {
    this.defineVariable(node.value, this.set, this.variables, null, def);
  }
```
</details>

##### `referenceDualValueType(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
public referenceDualValueType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type | ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>

##### `referenceType(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
public referenceType(node: TSESTree.Identifier): void {
    const ref = new Reference(
      node,
      this as Scope,
      ReferenceFlag.Read,
      null,
      null,
      false,
      ReferenceTypeFlag.Type,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>

##### `referenceValue(node: TSESTree.Identifier | TSESTree.JSXIdentifier, assign: ReferenceFlag, writeExpr: TSESTree.Expression | null, maybeImplicitGlobal: ReferenceImplicitGlobal | null, init: boolean): void`

<details><summary>Code</summary>

```ts
public referenceValue(
    node: TSESTree.Identifier | TSESTree.JSXIdentifier,
    assign: ReferenceFlag = ReferenceFlag.Read,
    writeExpr?: TSESTree.Expression | null,
    maybeImplicitGlobal?: ReferenceImplicitGlobal | null,
    init = false,
  ): void {
    const ref = new Reference(
      node,
      this as Scope,
      assign,
      writeExpr,
      maybeImplicitGlobal,
      init,
      ReferenceTypeFlag.Value,
    );

    this.references.push(ref);
    this.leftToResolve?.push(ref);
  }
```
</details>


---

## Type Aliases

### `VariableScope`

```ts
type VariableScope = FunctionScope | GlobalScope | ModuleScope | TSModuleScope;
```

### `AnyScope`

```ts
type AnyScope = ScopeBase<ScopeType, TSESTree.Node, Scope | null>;
```


---