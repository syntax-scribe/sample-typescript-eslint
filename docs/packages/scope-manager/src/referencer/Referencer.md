[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `Referencer.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 68
- **Classes**: 1
- **Imports**: 26
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/Referencer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Lib` | `@typescript-eslint/types` |
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `GlobalScope` | `../scope` |
| `Scope` | `../scope` |
| `ScopeManager` | `../ScopeManager` |
| `LibDefinition` | `../variable` |
| `ReferenceImplicitGlobal` | `./Reference` |
| `VisitorOptions` | `./Visitor` |
| `assert` | `../assert` |
| `CatchClauseDefinition` | `../definition` |
| `FunctionNameDefinition` | `../definition` |
| `ImportBindingDefinition` | `../definition` |
| `ParameterDefinition` | `../definition` |
| `TSEnumMemberDefinition` | `../definition` |
| `TSEnumNameDefinition` | `../definition` |
| `TSModuleNameDefinition` | `../definition` |
| `VariableDefinition` | `../definition` |
| `TSLibraries` | `../lib` |
| `ClassVisitor` | `./ClassVisitor` |
| `ExportVisitor` | `./ExportVisitor` |
| `ImportVisitor` | `./ImportVisitor` |
| `PatternVisitor` | `./PatternVisitor` |
| `ReferenceFlag` | `./Reference` |
| `TypeVisitor` | `./TypeVisitor` |
| `Visitor` | `./Visitor` |


---

## Functions

### `Referencer.populateGlobalsFromLib(globalScope: GlobalScope): void`

<details><summary>Code</summary>

```ts
private populateGlobalsFromLib(globalScope: GlobalScope): void {
    const flattenedLibs = new Set<LibDefinition>();
    for (const lib of this.#lib) {
      const definition = TSLibraries.get(lib);
      if (!definition) {
        throw new Error(`Invalid value for lib provided: ${lib}`);
      }
      flattenedLibs.add(definition);
    }

    // Flatten and deduplicate the set of included libs
    for (const lib of flattenedLibs) {
      // By adding the dependencies to the set as we iterate it,
      // they get iterated only if they are new
      for (const referencedLib of lib.libs) {
        flattenedLibs.add(referencedLib);
      }

      // This loop is guaranteed to see each included lib exactly once
      for (const [name, variable] of lib.variables) {
        globalScope.defineImplicitVariable(name, variable);
      }
    }

    // for const assertions (`{} as const` / `<const>{}`)
    globalScope.defineImplicitVariable('const', {
      eslintImplicitGlobalSetting: 'readonly',
      isTypeVariable: true,
      isValueVariable: false,
    });
  }
```
</details>

- **Parameters**:
  - `globalScope: GlobalScope`
- **Return Type**: `void`
- **Calls**:
  - `TSLibraries.get`
  - `flattenedLibs.add`
  - `globalScope.defineImplicitVariable`
- **Internal Comments**:
```
// Flatten and deduplicate the set of included libs
// By adding the dependencies to the set as we iterate it,
// they get iterated only if they are new
// This loop is guaranteed to see each included lib exactly once
// for const assertions (`{} as const` / `<const>{}`) (x4)
```

### `Referencer.close(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
public close(node: TSESTree.Node): void {
    while (this.currentScope(true) && node === this.currentScope().block) {
      this.scopeManager.currentScope = this.currentScope().close(
        this.scopeManager,
      );
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope`
  - `this.currentScope().close`
### `Referencer.currentScope(): Scope`

<details><summary>Code</summary>

```ts
public currentScope(): Scope;
```
</details>

- **Return Type**: `Scope`
### `Referencer.currentScope(throwOnNull: true): Scope | null`

<details><summary>Code</summary>

```ts
public currentScope(throwOnNull: true): Scope | null;
```
</details>

- **Parameters**:
  - `throwOnNull: true`
- **Return Type**: `Scope | null`
### `Referencer.currentScope(dontThrowOnNull: true): Scope | null`

<details><summary>Code</summary>

```ts
public currentScope(dontThrowOnNull?: true): Scope | null {
    if (!dontThrowOnNull) {
      assert(this.scopeManager.currentScope, 'aaa');
    }
    return this.scopeManager.currentScope;
  }
```
</details>

- **Parameters**:
  - `dontThrowOnNull: true`
- **Return Type**: `Scope | null`
- **Calls**:
  - `assert (from ../assert)`
### `Referencer.referencingDefaultValue(pattern: TSESTree.Identifier, assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[], maybeImplicitGlobal: ReferenceImplicitGlobal | null, init: boolean): void`

<details><summary>Code</summary>

```ts
public referencingDefaultValue(
    pattern: TSESTree.Identifier,
    assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[],
    maybeImplicitGlobal: ReferenceImplicitGlobal | null,
    init: boolean,
  ): void {
    assignments.forEach(assignment => {
      this.currentScope().referenceValue(
        pattern,
        ReferenceFlag.Write,
        assignment.right,
        maybeImplicitGlobal,
        init,
      );
    });
  }
```
</details>

- **Parameters**:
  - `pattern: TSESTree.Identifier`
  - `assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[]`
  - `maybeImplicitGlobal: ReferenceImplicitGlobal | null`
  - `init: boolean`
- **Return Type**: `void`
- **Calls**:
  - `assignments.forEach`
  - `this.currentScope().referenceValue`
### `Referencer.referenceInSomeUpperScope(name: string): boolean`

<details><summary>Code</summary>

```ts
private referenceInSomeUpperScope(name: string): boolean {
    let scope = this.scopeManager.currentScope;
    while (scope) {
      const variable = scope.set.get(name);
      if (!variable) {
        scope = scope.upper;
        continue;
      }

      scope.referenceValue(variable.identifiers[0]);
      return true;
    }

    return false;
  }
```
</details>

- **JSDoc**:
```ts
/**
   * Searches for a variable named "name" in the upper scopes and adds a pseudo-reference from itself to itself
   */
```

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `scope.set.get`
  - `scope.referenceValue`
### `Referencer.referenceJsxFragment(): void`

<details><summary>Code</summary>

```ts
private referenceJsxFragment(): void {
    if (
      this.#jsxFragmentName == null ||
      this.#hasReferencedJsxFragmentFactory
    ) {
      return;
    }
    this.#hasReferencedJsxFragmentFactory = this.referenceInSomeUpperScope(
      this.#jsxFragmentName,
    );
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `this.referenceInSomeUpperScope`
### `Referencer.referenceJsxPragma(): void`

<details><summary>Code</summary>

```ts
private referenceJsxPragma(): void {
    if (this.#jsxPragma == null || this.#hasReferencedJsxFactory) {
      return;
    }
    this.#hasReferencedJsxFactory = this.referenceInSomeUpperScope(
      this.#jsxPragma,
    );
  }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `this.referenceInSomeUpperScope`
### `Referencer.visitClass(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    ClassVisitor.visit(this, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
- **Return Type**: `void`
- **Calls**:
  - `ClassVisitor.visit`
### `Referencer.visitForIn(node: TSESTree.ForInStatement | TSESTree.ForOfStatement): void`

<details><summary>Code</summary>

```ts
protected visitForIn(
    node: TSESTree.ForInStatement | TSESTree.ForOfStatement,
  ): void {
    if (
      node.left.type === AST_NODE_TYPES.VariableDeclaration &&
      node.left.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    if (node.left.type === AST_NODE_TYPES.VariableDeclaration) {
      this.visit(node.left);
      this.visitPattern(node.left.declarations[0].id, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.Write,
          node.right,
          null,
          true,
        );
      });
    } else {
      this.visitPattern(
        node.left,
        (pattern, info) => {
          const maybeImplicitGlobal = !this.currentScope().isStrict
            ? {
                node,
                pattern,
              }
            : null;
          this.referencingDefaultValue(
            pattern,
            info.assignments,
            maybeImplicitGlobal,
            false,
          );
          this.currentScope().referenceValue(
            pattern,
            ReferenceFlag.Write,
            node.right,
            maybeImplicitGlobal,
            false,
          );
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.right);
    this.visit(node.body);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ForInStatement | TSESTree.ForOfStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestForScope`
  - `this.visit`
  - `this.visitPattern`
  - `this.currentScope().referenceValue`
  - `this.currentScope`
  - `this.referencingDefaultValue`
  - `this.close`
### `Referencer.visitFunction(node: | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected visitFunction(
    node:
      | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    // FunctionDeclaration name is defined in upper scope
    // NOTE: Not referring variableScope. It is intended.
    // Since
    //  in ES5, FunctionDeclaration should be in FunctionBody.
    //  in ES6, FunctionDeclaration should be block scoped.

    if (node.type === AST_NODE_TYPES.FunctionExpression) {
      if (node.id) {
        // FunctionExpression with name creates its special scope;
        // FunctionExpressionNameScope.
        this.scopeManager.nestFunctionExpressionNameScope(node);
      }
    } else if (node.id) {
      // id is defined in upper scope
      this.currentScope().defineIdentifier(
        node.id,
        new FunctionNameDefinition(node.id, node),
      );
    }

    // Consider this function is in the MethodDefinition.
    this.scopeManager.nestFunctionScope(node, false);

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
      param.decorators.forEach(d => this.visit(d));
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    // In TypeScript there are a number of function-like constructs which have no body,
    // so check it exists before traversing
    if (node.body) {
      // Skip BlockStatement to prevent creating BlockStatement scope.
      if (node.body.type === AST_NODE_TYPES.BlockStatement) {
        this.visitChildren(node.body);
      } else {
        this.visit(node.body);
      }
    }

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestFunctionExpressionNameScope`
  - `this.currentScope().defineIdentifier`
  - `this.scopeManager.nestFunctionScope`
  - `this.visitPattern`
  - `this.referencingDefaultValue`
  - `this.visitFunctionParameterTypeAnnotation`
  - `param.decorators.forEach`
  - `this.visit`
  - `this.visitType`
  - `this.visitChildren`
  - `this.close`
- **Internal Comments**:
```
// FunctionDeclaration name is defined in upper scope
// NOTE: Not referring variableScope. It is intended.
// Since
//  in ES5, FunctionDeclaration should be in FunctionBody.
//  in ES6, FunctionDeclaration should be block scoped.
// FunctionExpression with name creates its special scope; (x5)
// FunctionExpressionNameScope. (x5)
// id is defined in upper scope (x6)
// Consider this function is in the MethodDefinition. (x5)
// Process parameter declarations.
// In TypeScript there are a number of function-like constructs which have no body,
// so check it exists before traversing
// Skip BlockStatement to prevent creating BlockStatement scope.
```

### `Referencer.visitFunctionParameterTypeAnnotation(node: TSESTree.Parameter): void`

<details><summary>Code</summary>

```ts
protected visitFunctionParameterTypeAnnotation(
    node: TSESTree.Parameter,
  ): void {
    switch (node.type) {
      case AST_NODE_TYPES.AssignmentPattern:
        this.visitType(node.left.typeAnnotation);
        break;
      case AST_NODE_TYPES.TSParameterProperty:
        this.visitFunctionParameterTypeAnnotation(node.parameter);
        break;
      default:
        this.visitType(node.typeAnnotation);
        break;
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Parameter`
- **Return Type**: `void`
- **Calls**:
  - `this.visitType`
  - `this.visitFunctionParameterTypeAnnotation`
### `Referencer.visitJSXElement(node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement): void`

<details><summary>Code</summary>

```ts
protected visitJSXElement(
    node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement,
  ): void {
    if (node.name.type === AST_NODE_TYPES.JSXIdentifier) {
      if (
        node.name.name[0].toUpperCase() === node.name.name[0] ||
        node.name.name === 'this'
      ) {
        // lower cased component names are always treated as "intrinsic" names, and are converted to a string,
        // not a variable by JSX transforms:
        // <div /> => React.createElement("div", null)

        // the only case we want to visit a lower-cased component has its name as "this",
        this.visit(node.name);
      }
    } else {
      this.visit(node.name);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement`
- **Return Type**: `void`
- **Calls**:
  - `node.name.name[0].toUpperCase`
  - `this.visit`
- **Internal Comments**:
```
// lower cased component names are always treated as "intrinsic" names, and are converted to a string, (x4)
// not a variable by JSX transforms: (x4)
// <div /> => React.createElement("div", null) (x4)
// the only case we want to visit a lower-cased component has its name as "this", (x4)
```

### `Referencer.visitProperty(node: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected visitProperty(node: TSESTree.Property): void {
    if (node.computed) {
      this.visit(node.key);
    }

    this.visit(node.value);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Property`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `Referencer.visitType(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
protected visitType(node: TSESTree.Node | null | undefined): void {
    if (!node) {
      return;
    }
    TypeVisitor.visit(this, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `TypeVisitor.visit`
### `Referencer.visitTypeAssertion(node: | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion): void`

<details><summary>Code</summary>

```ts
protected visitTypeAssertion(
    node:
      | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion,
  ): void {
    this.visit(node.expression);
    this.visitType(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `this.visitType`
### `Referencer.ArrowFunctionExpression(node: TSESTree.ArrowFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected ArrowFunctionExpression(
    node: TSESTree.ArrowFunctionExpression,
  ): void {
    this.visitFunction(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ArrowFunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunction`
### `Referencer.AssignmentExpression(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    const left = this.visitExpressionTarget(node.left);

    if (PatternVisitor.isPattern(left)) {
      if (node.operator === '=') {
        this.visitPattern(
          left,
          (pattern, info) => {
            const maybeImplicitGlobal = !this.currentScope().isStrict
              ? {
                  node,
                  pattern,
                }
              : null;
            this.referencingDefaultValue(
              pattern,
              info.assignments,
              maybeImplicitGlobal,
              false,
            );
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              node.right,
              maybeImplicitGlobal,
              false,
            );
          },
          { processRightHandNodes: true },
        );
      } else if (left.type === AST_NODE_TYPES.Identifier) {
        this.currentScope().referenceValue(
          left,
          ReferenceFlag.ReadWrite,
          node.right,
        );
      }
    } else {
      this.visit(left);
    }
    this.visit(node.right);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.AssignmentExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitExpressionTarget`
  - `PatternVisitor.isPattern`
  - `this.visitPattern`
  - `this.currentScope`
  - `this.referencingDefaultValue`
  - `this.currentScope().referenceValue`
  - `this.visit`
### `Referencer.BlockStatement(node: TSESTree.BlockStatement): void`

<details><summary>Code</summary>

```ts
protected BlockStatement(node: TSESTree.BlockStatement): void {
    this.scopeManager.nestBlockScope(node);

    this.visitChildren(node);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.BlockStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestBlockScope`
  - `this.visitChildren`
  - `this.close`
### `Referencer.BreakStatement(): void`

<details><summary>Code</summary>

```ts
protected BreakStatement(): void {
    // don't reference the break statement's label
  }
```
</details>

- **Return Type**: `void`
### `Referencer.CallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
protected CallExpression(node: TSESTree.CallExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
  - `this.visitType`
### `Referencer.CatchClause(node: TSESTree.CatchClause): void`

<details><summary>Code</summary>

```ts
protected CatchClause(node: TSESTree.CatchClause): void {
    this.scopeManager.nestCatchScope(node);

    if (node.param) {
      const param = node.param;
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new CatchClauseDefinition(param, node),
          );
          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.body);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.CatchClause`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestCatchScope`
  - `this.visitPattern`
  - `this.currentScope().defineIdentifier`
  - `this.referencingDefaultValue`
  - `this.visit`
  - `this.close`
### `Referencer.ClassDeclaration(node: TSESTree.ClassDeclaration): void`

<details><summary>Code</summary>

```ts
protected ClassDeclaration(node: TSESTree.ClassDeclaration): void {
    this.visitClass(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitClass`
### `Referencer.ClassExpression(node: TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected ClassExpression(node: TSESTree.ClassExpression): void {
    this.visitClass(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitClass`
### `Referencer.ContinueStatement(): void`

<details><summary>Code</summary>

```ts
protected ContinueStatement(): void {
    // don't reference the continue statement's label
  }
```
</details>

- **Return Type**: `void`
### `Referencer.ExportAllDeclaration(): void`

<details><summary>Code</summary>

```ts
protected ExportAllDeclaration(): void {
    // this defines no local variables
  }
```
</details>

- **Return Type**: `void`
### `Referencer.ExportDefaultDeclaration(node: TSESTree.ExportDefaultDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      ExportVisitor.visit(this, node);
    } else {
      this.visit(node.declaration);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExportDefaultDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `ExportVisitor.visit`
  - `this.visit`
### `Referencer.ExportNamedDeclaration(node: TSESTree.ExportNamedDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.declaration) {
      this.visit(node.declaration);
    } else {
      ExportVisitor.visit(this, node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ExportNamedDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `ExportVisitor.visit`
### `Referencer.ForInStatement(node: TSESTree.ForInStatement): void`

<details><summary>Code</summary>

```ts
protected ForInStatement(node: TSESTree.ForInStatement): void {
    this.visitForIn(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ForInStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.visitForIn`
### `Referencer.ForOfStatement(node: TSESTree.ForOfStatement): void`

<details><summary>Code</summary>

```ts
protected ForOfStatement(node: TSESTree.ForOfStatement): void {
    this.visitForIn(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ForOfStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.visitForIn`
### `Referencer.ForStatement(node: TSESTree.ForStatement): void`

<details><summary>Code</summary>

```ts
protected ForStatement(node: TSESTree.ForStatement): void {
    // Create ForStatement declaration.
    // NOTE: In ES6, ForStatement dynamically generates per iteration environment. However, this is
    // a static analyzer, we only generate one scope for ForStatement.
    if (
      node.init &&
      node.init.type === AST_NODE_TYPES.VariableDeclaration &&
      node.init.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    this.visitChildren(node);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ForStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestForScope`
  - `this.visitChildren`
  - `this.close`
- **Internal Comments**:
```
// Create ForStatement declaration.
// NOTE: In ES6, ForStatement dynamically generates per iteration environment. However, this is
// a static analyzer, we only generate one scope for ForStatement.
```

### `Referencer.FunctionDeclaration(node: TSESTree.FunctionDeclaration): void`

<details><summary>Code</summary>

```ts
protected FunctionDeclaration(node: TSESTree.FunctionDeclaration): void {
    this.visitFunction(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.FunctionDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunction`
### `Referencer.FunctionExpression(node: TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
protected FunctionExpression(node: TSESTree.FunctionExpression): void {
    this.visitFunction(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.FunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunction`
### `Referencer.Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.currentScope().referenceValue(node);
    this.visitType(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().referenceValue`
  - `this.visitType`
### `Referencer.ImportAttribute(): void`

<details><summary>Code</summary>

```ts
protected ImportAttribute(): void {
    // import assertions are module metadata and thus have no variables to reference
  }
```
</details>

- **Return Type**: `void`
### `Referencer.ImportDeclaration(node: TSESTree.ImportDeclaration): void`

<details><summary>Code</summary>

```ts
protected ImportDeclaration(node: TSESTree.ImportDeclaration): void {
    assert(
      this.scopeManager.isModule(),
      'ImportDeclaration should appear when the mode is ES6 and in the module context.',
    );

    ImportVisitor.visit(this, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ImportDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `assert (from ../assert)`
  - `this.scopeManager.isModule`
  - `ImportVisitor.visit`
### `Referencer.JSXAttribute(node: TSESTree.JSXAttribute): void`

<details><summary>Code</summary>

```ts
protected JSXAttribute(node: TSESTree.JSXAttribute): void {
    this.visit(node.value);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXAttribute`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `Referencer.JSXClosingElement(node: TSESTree.JSXClosingElement): void`

<details><summary>Code</summary>

```ts
protected JSXClosingElement(node: TSESTree.JSXClosingElement): void {
    this.visitJSXElement(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXClosingElement`
- **Return Type**: `void`
- **Calls**:
  - `this.visitJSXElement`
### `Referencer.JSXFragment(node: TSESTree.JSXFragment): void`

<details><summary>Code</summary>

```ts
protected JSXFragment(node: TSESTree.JSXFragment): void {
    this.referenceJsxPragma();
    this.referenceJsxFragment();
    this.visitChildren(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXFragment`
- **Return Type**: `void`
- **Calls**:
  - `this.referenceJsxPragma`
  - `this.referenceJsxFragment`
  - `this.visitChildren`
### `Referencer.JSXIdentifier(node: TSESTree.JSXIdentifier): void`

<details><summary>Code</summary>

```ts
protected JSXIdentifier(node: TSESTree.JSXIdentifier): void {
    this.currentScope().referenceValue(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXIdentifier`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().referenceValue`
### `Referencer.JSXMemberExpression(node: TSESTree.JSXMemberExpression): void`

<details><summary>Code</summary>

```ts
protected JSXMemberExpression(node: TSESTree.JSXMemberExpression): void {
    if (
      node.object.type !== AST_NODE_TYPES.JSXIdentifier ||
      node.object.name !== 'this'
    ) {
      this.visit(node.object);
    }
    // we don't ever reference the property as it's always going to be a property on the thing
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXMemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `Referencer.JSXOpeningElement(node: TSESTree.JSXOpeningElement): void`

<details><summary>Code</summary>

```ts
protected JSXOpeningElement(node: TSESTree.JSXOpeningElement): void {
    this.referenceJsxPragma();
    this.visitJSXElement(node);
    this.visitType(node.typeArguments);
    for (const attr of node.attributes) {
      this.visit(attr);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.JSXOpeningElement`
- **Return Type**: `void`
- **Calls**:
  - `this.referenceJsxPragma`
  - `this.visitJSXElement`
  - `this.visitType`
  - `this.visit`
### `Referencer.LabeledStatement(node: TSESTree.LabeledStatement): void`

<details><summary>Code</summary>

```ts
protected LabeledStatement(node: TSESTree.LabeledStatement): void {
    this.visit(node.body);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.LabeledStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `Referencer.MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    if (node.computed) {
      this.visit(node.property);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `Referencer.MetaProperty(): void`

<details><summary>Code</summary>

```ts
protected MetaProperty(): void {
    // meta properties all builtin globals
  }
```
</details>

- **Return Type**: `void`
### `Referencer.NewExpression(node: TSESTree.NewExpression): void`

<details><summary>Code</summary>

```ts
protected NewExpression(node: TSESTree.NewExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.NewExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
  - `this.visitType`
### `Referencer.PrivateIdentifier(): void`

<details><summary>Code</summary>

```ts
protected PrivateIdentifier(): void {
    // private identifiers are members on classes and thus have no variables to reference
  }
```
</details>

- **Return Type**: `void`
### `Referencer.Program(node: TSESTree.Program): void`

<details><summary>Code</summary>

```ts
protected Program(node: TSESTree.Program): void {
    const globalScope = this.scopeManager.nestGlobalScope(node);
    this.populateGlobalsFromLib(globalScope);

    if (this.scopeManager.isGlobalReturn()) {
      // Force strictness of GlobalScope to false when using node.js scope.
      this.currentScope().isStrict = false;
      this.scopeManager.nestFunctionScope(node, false);
    }

    if (this.scopeManager.isModule()) {
      this.scopeManager.nestModuleScope(node);
    }

    if (this.scopeManager.isImpliedStrict()) {
      this.currentScope().isStrict = true;
    }

    this.visitChildren(node);
    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Program`
- **Return Type**: `void`
- **Calls**:
  - `this.scopeManager.nestGlobalScope`
  - `this.populateGlobalsFromLib`
  - `this.scopeManager.isGlobalReturn`
  - `this.currentScope`
  - `this.scopeManager.nestFunctionScope`
  - `this.scopeManager.isModule`
  - `this.scopeManager.nestModuleScope`
  - `this.scopeManager.isImpliedStrict`
  - `this.visitChildren`
  - `this.close`
- **Internal Comments**:
```
// Force strictness of GlobalScope to false when using node.js scope. (x6)
```

### `Referencer.Property(node: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected Property(node: TSESTree.Property): void {
    this.visitProperty(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Property`
- **Return Type**: `void`
- **Calls**:
  - `this.visitProperty`
### `Referencer.SwitchStatement(node: TSESTree.SwitchStatement): void`

<details><summary>Code</summary>

```ts
protected SwitchStatement(node: TSESTree.SwitchStatement): void {
    this.visit(node.discriminant);

    this.scopeManager.nestSwitchScope(node);

    for (const switchCase of node.cases) {
      this.visit(switchCase);
    }

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.SwitchStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `this.scopeManager.nestSwitchScope`
  - `this.close`
### `Referencer.TaggedTemplateExpression(node: TSESTree.TaggedTemplateExpression): void`

<details><summary>Code</summary>

```ts
protected TaggedTemplateExpression(
    node: TSESTree.TaggedTemplateExpression,
  ): void {
    this.visit(node.tag);
    this.visit(node.quasi);
    this.visitType(node.typeArguments);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TaggedTemplateExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `this.visitType`
### `Referencer.TSAsExpression(node: TSESTree.TSAsExpression): void`

<details><summary>Code</summary>

```ts
protected TSAsExpression(node: TSESTree.TSAsExpression): void {
    this.visitTypeAssertion(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAsExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitTypeAssertion`
### `Referencer.TSDeclareFunction(node: TSESTree.TSDeclareFunction): void`

<details><summary>Code</summary>

```ts
protected TSDeclareFunction(node: TSESTree.TSDeclareFunction): void {
    this.visitFunction(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSDeclareFunction`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunction`
### `Referencer.TSEmptyBodyFunctionExpression(node: TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected TSEmptyBodyFunctionExpression(
    node: TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    this.visitFunction(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEmptyBodyFunctionExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunction`
### `Referencer.TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void {
    this.currentScope().defineIdentifier(
      node.id,
      new TSEnumNameDefinition(node.id, node),
    );

    // enum members can be referenced within the enum body
    this.scopeManager.nestTSEnumScope(node);

    for (const member of node.body.members) {
      // TS resolves literal named members to be actual names
      // enum Foo {
      //   'a' = 1,
      //   b = a, // this references the 'a' member
      // }
      if (
        member.id.type === AST_NODE_TYPES.Literal &&
        typeof member.id.value === 'string'
      ) {
        const name = member.id;
        this.currentScope().defineLiteralIdentifier(
          name,
          new TSEnumMemberDefinition(name, member),
        );
      } else if (
        !member.computed &&
        member.id.type === AST_NODE_TYPES.Identifier
      ) {
        this.currentScope().defineIdentifier(
          member.id,
          new TSEnumMemberDefinition(member.id, member),
        );
      }

      this.visit(member.initializer);
    }

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().defineIdentifier`
  - `this.scopeManager.nestTSEnumScope`
  - `this.currentScope().defineLiteralIdentifier`
  - `this.visit`
  - `this.close`
- **Internal Comments**:
```
// enum members can be referenced within the enum body (x5)
// TS resolves literal named members to be actual names
// enum Foo {
//   'a' = 1,
//   b = a, // this references the 'a' member
// }
```

### `Referencer.TSExportAssignment(node: TSESTree.TSExportAssignment): void`

<details><summary>Code</summary>

```ts
protected TSExportAssignment(node: TSESTree.TSExportAssignment): void {
    if (node.expression.type === AST_NODE_TYPES.Identifier) {
      // this is a special case - you can `export = T` where `T` is a type OR a
      // value however `T[U]` is illegal when `T` is a type and `T.U` is illegal
      // when `T.U` is a type
      // i.e. if the expression is JUST an Identifier - it could be either ref
      // kind; otherwise the standard rules apply
      this.currentScope().referenceDualValueType(node.expression);
    } else {
      this.visit(node.expression);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSExportAssignment`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().referenceDualValueType`
  - `this.visit`
- **Internal Comments**:
```
// this is a special case - you can `export = T` where `T` is a type OR a (x6)
// value however `T[U]` is illegal when `T` is a type and `T.U` is illegal (x6)
// when `T.U` is a type (x6)
// i.e. if the expression is JUST an Identifier - it could be either ref (x6)
// kind; otherwise the standard rules apply (x6)
```

### `Referencer.TSImportEqualsDeclaration(node: TSESTree.TSImportEqualsDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSImportEqualsDeclaration(
    node: TSESTree.TSImportEqualsDeclaration,
  ): void {
    this.currentScope().defineIdentifier(
      node.id,
      new ImportBindingDefinition(node.id, node, node),
    );

    if (node.moduleReference.type === AST_NODE_TYPES.TSQualifiedName) {
      let moduleIdentifier = node.moduleReference.left;
      while (moduleIdentifier.type === AST_NODE_TYPES.TSQualifiedName) {
        moduleIdentifier = moduleIdentifier.left;
      }
      this.visit(moduleIdentifier);
    } else {
      this.visit(node.moduleReference);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSImportEqualsDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().defineIdentifier`
  - `this.visit`
### `Referencer.TSInstantiationExpression(node: TSESTree.TSInstantiationExpression): void`

<details><summary>Code</summary>

```ts
protected TSInstantiationExpression(
    node: TSESTree.TSInstantiationExpression,
  ): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSInstantiationExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
  - `this.visitType`
### `Referencer.TSInterfaceDeclaration(node: TSESTree.TSInterfaceDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.visitType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSInterfaceDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitType`
### `Referencer.TSModuleDeclaration(node: TSESTree.TSModuleDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSModuleDeclaration(node: TSESTree.TSModuleDeclaration): void {
    if (node.id.type === AST_NODE_TYPES.Identifier && node.kind !== 'global') {
      this.currentScope().defineIdentifier(
        node.id,
        new TSModuleNameDefinition(node.id, node),
      );
    }

    this.scopeManager.nestTSModuleScope(node);

    this.visit(node.body);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSModuleDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope().defineIdentifier`
  - `this.scopeManager.nestTSModuleScope`
  - `this.visit`
  - `this.close`
### `Referencer.TSSatisfiesExpression(node: TSESTree.TSSatisfiesExpression): void`

<details><summary>Code</summary>

```ts
protected TSSatisfiesExpression(node: TSESTree.TSSatisfiesExpression): void {
    this.visitTypeAssertion(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSSatisfiesExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitTypeAssertion`
### `Referencer.TSTypeAliasDeclaration(node: TSESTree.TSTypeAliasDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.visitType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeAliasDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitType`
### `Referencer.TSTypeAssertion(node: TSESTree.TSTypeAssertion): void`

<details><summary>Code</summary>

```ts
protected TSTypeAssertion(node: TSESTree.TSTypeAssertion): void {
    this.visitTypeAssertion(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeAssertion`
- **Return Type**: `void`
- **Calls**:
  - `this.visitTypeAssertion`
### `Referencer.UpdateExpression(node: TSESTree.UpdateExpression): void`

<details><summary>Code</summary>

```ts
protected UpdateExpression(node: TSESTree.UpdateExpression): void {
    const argument = this.visitExpressionTarget(node.argument);

    if (PatternVisitor.isPattern(argument)) {
      this.visitPattern(argument, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.ReadWrite,
          null,
        );
      });
    } else {
      this.visitChildren(node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.UpdateExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visitExpressionTarget`
  - `PatternVisitor.isPattern`
  - `this.visitPattern`
  - `this.currentScope().referenceValue`
  - `this.visitChildren`
### `Referencer.VariableDeclaration(node: TSESTree.VariableDeclaration): void`

<details><summary>Code</summary>

```ts
protected VariableDeclaration(node: TSESTree.VariableDeclaration): void {
    const variableTargetScope =
      node.kind === 'var'
        ? this.currentScope().variableScope
        : this.currentScope();

    for (const decl of node.declarations) {
      const init = decl.init;

      this.visitPattern(
        decl.id,
        (pattern, info) => {
          variableTargetScope.defineIdentifier(
            pattern,
            new VariableDefinition(pattern, decl, node),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
          if (init) {
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              init,
              null,
              true,
            );
          }
        },
        { processRightHandNodes: true },
      );

      this.visit(decl.init);
      this.visitType(decl.id.typeAnnotation);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.VariableDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.currentScope`
  - `this.visitPattern`
  - `variableTargetScope.defineIdentifier`
  - `this.referencingDefaultValue`
  - `this.currentScope().referenceValue`
  - `this.visit`
  - `this.visitType`
### `Referencer.WithStatement(node: TSESTree.WithStatement): void`

<details><summary>Code</summary>

```ts
protected WithStatement(node: TSESTree.WithStatement): void {
    this.visit(node.object);

    // Then nest scope for WithStatement.
    this.scopeManager.nestWithScope(node);

    this.visit(node.body);

    this.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.WithStatement`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `this.scopeManager.nestWithScope`
  - `this.close`
- **Internal Comments**:
```
// Then nest scope for WithStatement. (x5)
```

### `Referencer.visitExpressionTarget(left: TSESTree.Node): TSESTree.Node`

<details><summary>Code</summary>

```ts
private visitExpressionTarget(left: TSESTree.Node) {
    switch (left.type) {
      case AST_NODE_TYPES.TSAsExpression:
      case AST_NODE_TYPES.TSTypeAssertion:
        // explicitly visit the type annotation
        this.visitType(left.typeAnnotation);
      // intentional fallthrough
      case AST_NODE_TYPES.TSNonNullExpression:
        // unwrap the expression
        left = left.expression;
    }

    return left;
  }
```
</details>

- **Parameters**:
  - `left: TSESTree.Node`
- **Return Type**: `TSESTree.Node`
- **Calls**:
  - `this.visitType`
- **Internal Comments**:
```
// explicitly visit the type annotation (x4)
// intentional fallthrough
// unwrap the expression (x3)
```


---

## Classes

### `Referencer`

<details><summary>Class Code</summary>

```ts
export class Referencer extends Visitor {
  #hasReferencedJsxFactory = false;
  #hasReferencedJsxFragmentFactory = false;
  #jsxFragmentName: string | null;
  #jsxPragma: string | null;
  #lib: Lib[];
  public readonly scopeManager: ScopeManager;

  constructor(options: ReferencerOptions, scopeManager: ScopeManager) {
    super(options);
    this.scopeManager = scopeManager;
    this.#jsxPragma = options.jsxPragma;
    this.#jsxFragmentName = options.jsxFragmentName;
    this.#lib = options.lib;
  }

  private populateGlobalsFromLib(globalScope: GlobalScope): void {
    const flattenedLibs = new Set<LibDefinition>();
    for (const lib of this.#lib) {
      const definition = TSLibraries.get(lib);
      if (!definition) {
        throw new Error(`Invalid value for lib provided: ${lib}`);
      }
      flattenedLibs.add(definition);
    }

    // Flatten and deduplicate the set of included libs
    for (const lib of flattenedLibs) {
      // By adding the dependencies to the set as we iterate it,
      // they get iterated only if they are new
      for (const referencedLib of lib.libs) {
        flattenedLibs.add(referencedLib);
      }

      // This loop is guaranteed to see each included lib exactly once
      for (const [name, variable] of lib.variables) {
        globalScope.defineImplicitVariable(name, variable);
      }
    }

    // for const assertions (`{} as const` / `<const>{}`)
    globalScope.defineImplicitVariable('const', {
      eslintImplicitGlobalSetting: 'readonly',
      isTypeVariable: true,
      isValueVariable: false,
    });
  }
  public close(node: TSESTree.Node): void {
    while (this.currentScope(true) && node === this.currentScope().block) {
      this.scopeManager.currentScope = this.currentScope().close(
        this.scopeManager,
      );
    }
  }
  public currentScope(): Scope;
  public currentScope(throwOnNull: true): Scope | null;
  public currentScope(dontThrowOnNull?: true): Scope | null {
    if (!dontThrowOnNull) {
      assert(this.scopeManager.currentScope, 'aaa');
    }
    return this.scopeManager.currentScope;
  }

  public referencingDefaultValue(
    pattern: TSESTree.Identifier,
    assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[],
    maybeImplicitGlobal: ReferenceImplicitGlobal | null,
    init: boolean,
  ): void {
    assignments.forEach(assignment => {
      this.currentScope().referenceValue(
        pattern,
        ReferenceFlag.Write,
        assignment.right,
        maybeImplicitGlobal,
        init,
      );
    });
  }

  /**
   * Searches for a variable named "name" in the upper scopes and adds a pseudo-reference from itself to itself
   */
  private referenceInSomeUpperScope(name: string): boolean {
    let scope = this.scopeManager.currentScope;
    while (scope) {
      const variable = scope.set.get(name);
      if (!variable) {
        scope = scope.upper;
        continue;
      }

      scope.referenceValue(variable.identifiers[0]);
      return true;
    }

    return false;
  }

  private referenceJsxFragment(): void {
    if (
      this.#jsxFragmentName == null ||
      this.#hasReferencedJsxFragmentFactory
    ) {
      return;
    }
    this.#hasReferencedJsxFragmentFactory = this.referenceInSomeUpperScope(
      this.#jsxFragmentName,
    );
  }

  private referenceJsxPragma(): void {
    if (this.#jsxPragma == null || this.#hasReferencedJsxFactory) {
      return;
    }
    this.#hasReferencedJsxFactory = this.referenceInSomeUpperScope(
      this.#jsxPragma,
    );
  }

  ///////////////////
  // Visit helpers //
  ///////////////////

  protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    ClassVisitor.visit(this, node);
  }

  protected visitForIn(
    node: TSESTree.ForInStatement | TSESTree.ForOfStatement,
  ): void {
    if (
      node.left.type === AST_NODE_TYPES.VariableDeclaration &&
      node.left.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    if (node.left.type === AST_NODE_TYPES.VariableDeclaration) {
      this.visit(node.left);
      this.visitPattern(node.left.declarations[0].id, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.Write,
          node.right,
          null,
          true,
        );
      });
    } else {
      this.visitPattern(
        node.left,
        (pattern, info) => {
          const maybeImplicitGlobal = !this.currentScope().isStrict
            ? {
                node,
                pattern,
              }
            : null;
          this.referencingDefaultValue(
            pattern,
            info.assignments,
            maybeImplicitGlobal,
            false,
          );
          this.currentScope().referenceValue(
            pattern,
            ReferenceFlag.Write,
            node.right,
            maybeImplicitGlobal,
            false,
          );
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.right);
    this.visit(node.body);

    this.close(node);
  }

  protected visitFunction(
    node:
      | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    // FunctionDeclaration name is defined in upper scope
    // NOTE: Not referring variableScope. It is intended.
    // Since
    //  in ES5, FunctionDeclaration should be in FunctionBody.
    //  in ES6, FunctionDeclaration should be block scoped.

    if (node.type === AST_NODE_TYPES.FunctionExpression) {
      if (node.id) {
        // FunctionExpression with name creates its special scope;
        // FunctionExpressionNameScope.
        this.scopeManager.nestFunctionExpressionNameScope(node);
      }
    } else if (node.id) {
      // id is defined in upper scope
      this.currentScope().defineIdentifier(
        node.id,
        new FunctionNameDefinition(node.id, node),
      );
    }

    // Consider this function is in the MethodDefinition.
    this.scopeManager.nestFunctionScope(node, false);

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
      param.decorators.forEach(d => this.visit(d));
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    // In TypeScript there are a number of function-like constructs which have no body,
    // so check it exists before traversing
    if (node.body) {
      // Skip BlockStatement to prevent creating BlockStatement scope.
      if (node.body.type === AST_NODE_TYPES.BlockStatement) {
        this.visitChildren(node.body);
      } else {
        this.visit(node.body);
      }
    }

    this.close(node);
  }
  protected visitFunctionParameterTypeAnnotation(
    node: TSESTree.Parameter,
  ): void {
    switch (node.type) {
      case AST_NODE_TYPES.AssignmentPattern:
        this.visitType(node.left.typeAnnotation);
        break;
      case AST_NODE_TYPES.TSParameterProperty:
        this.visitFunctionParameterTypeAnnotation(node.parameter);
        break;
      default:
        this.visitType(node.typeAnnotation);
        break;
    }
  }

  protected visitJSXElement(
    node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement,
  ): void {
    if (node.name.type === AST_NODE_TYPES.JSXIdentifier) {
      if (
        node.name.name[0].toUpperCase() === node.name.name[0] ||
        node.name.name === 'this'
      ) {
        // lower cased component names are always treated as "intrinsic" names, and are converted to a string,
        // not a variable by JSX transforms:
        // <div /> => React.createElement("div", null)

        // the only case we want to visit a lower-cased component has its name as "this",
        this.visit(node.name);
      }
    } else {
      this.visit(node.name);
    }
  }

  protected visitProperty(node: TSESTree.Property): void {
    if (node.computed) {
      this.visit(node.key);
    }

    this.visit(node.value);
  }

  protected visitType(node: TSESTree.Node | null | undefined): void {
    if (!node) {
      return;
    }
    TypeVisitor.visit(this, node);
  }

  protected visitTypeAssertion(
    node:
      | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion,
  ): void {
    this.visit(node.expression);
    this.visitType(node.typeAnnotation);
  }

  /////////////////////
  // Visit selectors //
  /////////////////////

  protected ArrowFunctionExpression(
    node: TSESTree.ArrowFunctionExpression,
  ): void {
    this.visitFunction(node);
  }

  protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    const left = this.visitExpressionTarget(node.left);

    if (PatternVisitor.isPattern(left)) {
      if (node.operator === '=') {
        this.visitPattern(
          left,
          (pattern, info) => {
            const maybeImplicitGlobal = !this.currentScope().isStrict
              ? {
                  node,
                  pattern,
                }
              : null;
            this.referencingDefaultValue(
              pattern,
              info.assignments,
              maybeImplicitGlobal,
              false,
            );
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              node.right,
              maybeImplicitGlobal,
              false,
            );
          },
          { processRightHandNodes: true },
        );
      } else if (left.type === AST_NODE_TYPES.Identifier) {
        this.currentScope().referenceValue(
          left,
          ReferenceFlag.ReadWrite,
          node.right,
        );
      }
    } else {
      this.visit(left);
    }
    this.visit(node.right);
  }

  protected BlockStatement(node: TSESTree.BlockStatement): void {
    this.scopeManager.nestBlockScope(node);

    this.visitChildren(node);

    this.close(node);
  }

  protected BreakStatement(): void {
    // don't reference the break statement's label
  }

  protected CallExpression(node: TSESTree.CallExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }

  protected CatchClause(node: TSESTree.CatchClause): void {
    this.scopeManager.nestCatchScope(node);

    if (node.param) {
      const param = node.param;
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new CatchClauseDefinition(param, node),
          );
          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.body);

    this.close(node);
  }

  protected ClassDeclaration(node: TSESTree.ClassDeclaration): void {
    this.visitClass(node);
  }

  protected ClassExpression(node: TSESTree.ClassExpression): void {
    this.visitClass(node);
  }

  protected ContinueStatement(): void {
    // don't reference the continue statement's label
  }

  protected ExportAllDeclaration(): void {
    // this defines no local variables
  }

  protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      ExportVisitor.visit(this, node);
    } else {
      this.visit(node.declaration);
    }
  }

  protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.declaration) {
      this.visit(node.declaration);
    } else {
      ExportVisitor.visit(this, node);
    }
  }

  protected ForInStatement(node: TSESTree.ForInStatement): void {
    this.visitForIn(node);
  }

  protected ForOfStatement(node: TSESTree.ForOfStatement): void {
    this.visitForIn(node);
  }

  protected ForStatement(node: TSESTree.ForStatement): void {
    // Create ForStatement declaration.
    // NOTE: In ES6, ForStatement dynamically generates per iteration environment. However, this is
    // a static analyzer, we only generate one scope for ForStatement.
    if (
      node.init &&
      node.init.type === AST_NODE_TYPES.VariableDeclaration &&
      node.init.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    this.visitChildren(node);

    this.close(node);
  }

  protected FunctionDeclaration(node: TSESTree.FunctionDeclaration): void {
    this.visitFunction(node);
  }

  protected FunctionExpression(node: TSESTree.FunctionExpression): void {
    this.visitFunction(node);
  }

  protected Identifier(node: TSESTree.Identifier): void {
    this.currentScope().referenceValue(node);
    this.visitType(node.typeAnnotation);
  }

  protected ImportAttribute(): void {
    // import assertions are module metadata and thus have no variables to reference
  }

  protected ImportDeclaration(node: TSESTree.ImportDeclaration): void {
    assert(
      this.scopeManager.isModule(),
      'ImportDeclaration should appear when the mode is ES6 and in the module context.',
    );

    ImportVisitor.visit(this, node);
  }

  protected JSXAttribute(node: TSESTree.JSXAttribute): void {
    this.visit(node.value);
  }

  protected JSXClosingElement(node: TSESTree.JSXClosingElement): void {
    this.visitJSXElement(node);
  }

  protected JSXFragment(node: TSESTree.JSXFragment): void {
    this.referenceJsxPragma();
    this.referenceJsxFragment();
    this.visitChildren(node);
  }

  protected JSXIdentifier(node: TSESTree.JSXIdentifier): void {
    this.currentScope().referenceValue(node);
  }

  protected JSXMemberExpression(node: TSESTree.JSXMemberExpression): void {
    if (
      node.object.type !== AST_NODE_TYPES.JSXIdentifier ||
      node.object.name !== 'this'
    ) {
      this.visit(node.object);
    }
    // we don't ever reference the property as it's always going to be a property on the thing
  }
  protected JSXOpeningElement(node: TSESTree.JSXOpeningElement): void {
    this.referenceJsxPragma();
    this.visitJSXElement(node);
    this.visitType(node.typeArguments);
    for (const attr of node.attributes) {
      this.visit(attr);
    }
  }

  protected LabeledStatement(node: TSESTree.LabeledStatement): void {
    this.visit(node.body);
  }

  protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    if (node.computed) {
      this.visit(node.property);
    }
  }

  protected MetaProperty(): void {
    // meta properties all builtin globals
  }

  protected NewExpression(node: TSESTree.NewExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }

  protected PrivateIdentifier(): void {
    // private identifiers are members on classes and thus have no variables to reference
  }

  protected Program(node: TSESTree.Program): void {
    const globalScope = this.scopeManager.nestGlobalScope(node);
    this.populateGlobalsFromLib(globalScope);

    if (this.scopeManager.isGlobalReturn()) {
      // Force strictness of GlobalScope to false when using node.js scope.
      this.currentScope().isStrict = false;
      this.scopeManager.nestFunctionScope(node, false);
    }

    if (this.scopeManager.isModule()) {
      this.scopeManager.nestModuleScope(node);
    }

    if (this.scopeManager.isImpliedStrict()) {
      this.currentScope().isStrict = true;
    }

    this.visitChildren(node);
    this.close(node);
  }

  protected Property(node: TSESTree.Property): void {
    this.visitProperty(node);
  }

  protected SwitchStatement(node: TSESTree.SwitchStatement): void {
    this.visit(node.discriminant);

    this.scopeManager.nestSwitchScope(node);

    for (const switchCase of node.cases) {
      this.visit(switchCase);
    }

    this.close(node);
  }

  protected TaggedTemplateExpression(
    node: TSESTree.TaggedTemplateExpression,
  ): void {
    this.visit(node.tag);
    this.visit(node.quasi);
    this.visitType(node.typeArguments);
  }

  protected TSAsExpression(node: TSESTree.TSAsExpression): void {
    this.visitTypeAssertion(node);
  }

  protected TSDeclareFunction(node: TSESTree.TSDeclareFunction): void {
    this.visitFunction(node);
  }

  protected TSEmptyBodyFunctionExpression(
    node: TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    this.visitFunction(node);
  }

  protected TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void {
    this.currentScope().defineIdentifier(
      node.id,
      new TSEnumNameDefinition(node.id, node),
    );

    // enum members can be referenced within the enum body
    this.scopeManager.nestTSEnumScope(node);

    for (const member of node.body.members) {
      // TS resolves literal named members to be actual names
      // enum Foo {
      //   'a' = 1,
      //   b = a, // this references the 'a' member
      // }
      if (
        member.id.type === AST_NODE_TYPES.Literal &&
        typeof member.id.value === 'string'
      ) {
        const name = member.id;
        this.currentScope().defineLiteralIdentifier(
          name,
          new TSEnumMemberDefinition(name, member),
        );
      } else if (
        !member.computed &&
        member.id.type === AST_NODE_TYPES.Identifier
      ) {
        this.currentScope().defineIdentifier(
          member.id,
          new TSEnumMemberDefinition(member.id, member),
        );
      }

      this.visit(member.initializer);
    }

    this.close(node);
  }

  protected TSExportAssignment(node: TSESTree.TSExportAssignment): void {
    if (node.expression.type === AST_NODE_TYPES.Identifier) {
      // this is a special case - you can `export = T` where `T` is a type OR a
      // value however `T[U]` is illegal when `T` is a type and `T.U` is illegal
      // when `T.U` is a type
      // i.e. if the expression is JUST an Identifier - it could be either ref
      // kind; otherwise the standard rules apply
      this.currentScope().referenceDualValueType(node.expression);
    } else {
      this.visit(node.expression);
    }
  }

  protected TSImportEqualsDeclaration(
    node: TSESTree.TSImportEqualsDeclaration,
  ): void {
    this.currentScope().defineIdentifier(
      node.id,
      new ImportBindingDefinition(node.id, node, node),
    );

    if (node.moduleReference.type === AST_NODE_TYPES.TSQualifiedName) {
      let moduleIdentifier = node.moduleReference.left;
      while (moduleIdentifier.type === AST_NODE_TYPES.TSQualifiedName) {
        moduleIdentifier = moduleIdentifier.left;
      }
      this.visit(moduleIdentifier);
    } else {
      this.visit(node.moduleReference);
    }
  }

  protected TSInstantiationExpression(
    node: TSESTree.TSInstantiationExpression,
  ): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }

  protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.visitType(node);
  }

  protected TSModuleDeclaration(node: TSESTree.TSModuleDeclaration): void {
    if (node.id.type === AST_NODE_TYPES.Identifier && node.kind !== 'global') {
      this.currentScope().defineIdentifier(
        node.id,
        new TSModuleNameDefinition(node.id, node),
      );
    }

    this.scopeManager.nestTSModuleScope(node);

    this.visit(node.body);

    this.close(node);
  }

  protected TSSatisfiesExpression(node: TSESTree.TSSatisfiesExpression): void {
    this.visitTypeAssertion(node);
  }

  protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.visitType(node);
  }

  protected TSTypeAssertion(node: TSESTree.TSTypeAssertion): void {
    this.visitTypeAssertion(node);
  }

  protected UpdateExpression(node: TSESTree.UpdateExpression): void {
    const argument = this.visitExpressionTarget(node.argument);

    if (PatternVisitor.isPattern(argument)) {
      this.visitPattern(argument, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.ReadWrite,
          null,
        );
      });
    } else {
      this.visitChildren(node);
    }
  }

  protected VariableDeclaration(node: TSESTree.VariableDeclaration): void {
    const variableTargetScope =
      node.kind === 'var'
        ? this.currentScope().variableScope
        : this.currentScope();

    for (const decl of node.declarations) {
      const init = decl.init;

      this.visitPattern(
        decl.id,
        (pattern, info) => {
          variableTargetScope.defineIdentifier(
            pattern,
            new VariableDefinition(pattern, decl, node),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
          if (init) {
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              init,
              null,
              true,
            );
          }
        },
        { processRightHandNodes: true },
      );

      this.visit(decl.init);
      this.visitType(decl.id.typeAnnotation);
    }
  }

  protected WithStatement(node: TSESTree.WithStatement): void {
    this.visit(node.object);

    // Then nest scope for WithStatement.
    this.scopeManager.nestWithScope(node);

    this.visit(node.body);

    this.close(node);
  }

  private visitExpressionTarget(left: TSESTree.Node) {
    switch (left.type) {
      case AST_NODE_TYPES.TSAsExpression:
      case AST_NODE_TYPES.TSTypeAssertion:
        // explicitly visit the type annotation
        this.visitType(left.typeAnnotation);
      // intentional fallthrough
      case AST_NODE_TYPES.TSNonNullExpression:
        // unwrap the expression
        left = left.expression;
    }

    return left;
  }
}
```
</details>

#### Methods

##### `populateGlobalsFromLib(globalScope: GlobalScope): void`

<details><summary>Code</summary>

```ts
private populateGlobalsFromLib(globalScope: GlobalScope): void {
    const flattenedLibs = new Set<LibDefinition>();
    for (const lib of this.#lib) {
      const definition = TSLibraries.get(lib);
      if (!definition) {
        throw new Error(`Invalid value for lib provided: ${lib}`);
      }
      flattenedLibs.add(definition);
    }

    // Flatten and deduplicate the set of included libs
    for (const lib of flattenedLibs) {
      // By adding the dependencies to the set as we iterate it,
      // they get iterated only if they are new
      for (const referencedLib of lib.libs) {
        flattenedLibs.add(referencedLib);
      }

      // This loop is guaranteed to see each included lib exactly once
      for (const [name, variable] of lib.variables) {
        globalScope.defineImplicitVariable(name, variable);
      }
    }

    // for const assertions (`{} as const` / `<const>{}`)
    globalScope.defineImplicitVariable('const', {
      eslintImplicitGlobalSetting: 'readonly',
      isTypeVariable: true,
      isValueVariable: false,
    });
  }
```
</details>

##### `close(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
public close(node: TSESTree.Node): void {
    while (this.currentScope(true) && node === this.currentScope().block) {
      this.scopeManager.currentScope = this.currentScope().close(
        this.scopeManager,
      );
    }
  }
```
</details>

##### `currentScope(): Scope`

<details><summary>Code</summary>

```ts
public currentScope(): Scope;
```
</details>

##### `currentScope(throwOnNull: true): Scope | null`

<details><summary>Code</summary>

```ts
public currentScope(throwOnNull: true): Scope | null;
```
</details>

##### `currentScope(dontThrowOnNull: true): Scope | null`

<details><summary>Code</summary>

```ts
public currentScope(dontThrowOnNull?: true): Scope | null {
    if (!dontThrowOnNull) {
      assert(this.scopeManager.currentScope, 'aaa');
    }
    return this.scopeManager.currentScope;
  }
```
</details>

##### `referencingDefaultValue(pattern: TSESTree.Identifier, assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[], maybeImplicitGlobal: ReferenceImplicitGlobal | null, init: boolean): void`

<details><summary>Code</summary>

```ts
public referencingDefaultValue(
    pattern: TSESTree.Identifier,
    assignments: (TSESTree.AssignmentExpression | TSESTree.AssignmentPattern)[],
    maybeImplicitGlobal: ReferenceImplicitGlobal | null,
    init: boolean,
  ): void {
    assignments.forEach(assignment => {
      this.currentScope().referenceValue(
        pattern,
        ReferenceFlag.Write,
        assignment.right,
        maybeImplicitGlobal,
        init,
      );
    });
  }
```
</details>

##### `referenceInSomeUpperScope(name: string): boolean`

<details><summary>Code</summary>

```ts
private referenceInSomeUpperScope(name: string): boolean {
    let scope = this.scopeManager.currentScope;
    while (scope) {
      const variable = scope.set.get(name);
      if (!variable) {
        scope = scope.upper;
        continue;
      }

      scope.referenceValue(variable.identifiers[0]);
      return true;
    }

    return false;
  }
```
</details>

##### `referenceJsxFragment(): void`

<details><summary>Code</summary>

```ts
private referenceJsxFragment(): void {
    if (
      this.#jsxFragmentName == null ||
      this.#hasReferencedJsxFragmentFactory
    ) {
      return;
    }
    this.#hasReferencedJsxFragmentFactory = this.referenceInSomeUpperScope(
      this.#jsxFragmentName,
    );
  }
```
</details>

##### `referenceJsxPragma(): void`

<details><summary>Code</summary>

```ts
private referenceJsxPragma(): void {
    if (this.#jsxPragma == null || this.#hasReferencedJsxFactory) {
      return;
    }
    this.#hasReferencedJsxFactory = this.referenceInSomeUpperScope(
      this.#jsxPragma,
    );
  }
```
</details>

##### `visitClass(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    ClassVisitor.visit(this, node);
  }
```
</details>

##### `visitForIn(node: TSESTree.ForInStatement | TSESTree.ForOfStatement): void`

<details><summary>Code</summary>

```ts
protected visitForIn(
    node: TSESTree.ForInStatement | TSESTree.ForOfStatement,
  ): void {
    if (
      node.left.type === AST_NODE_TYPES.VariableDeclaration &&
      node.left.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    if (node.left.type === AST_NODE_TYPES.VariableDeclaration) {
      this.visit(node.left);
      this.visitPattern(node.left.declarations[0].id, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.Write,
          node.right,
          null,
          true,
        );
      });
    } else {
      this.visitPattern(
        node.left,
        (pattern, info) => {
          const maybeImplicitGlobal = !this.currentScope().isStrict
            ? {
                node,
                pattern,
              }
            : null;
          this.referencingDefaultValue(
            pattern,
            info.assignments,
            maybeImplicitGlobal,
            false,
          );
          this.currentScope().referenceValue(
            pattern,
            ReferenceFlag.Write,
            node.right,
            maybeImplicitGlobal,
            false,
          );
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.right);
    this.visit(node.body);

    this.close(node);
  }
```
</details>

##### `visitFunction(node: | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected visitFunction(
    node:
      | TSESTree.ArrowFunctionExpression
      | TSESTree.FunctionDeclaration
      | TSESTree.FunctionExpression
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    // FunctionDeclaration name is defined in upper scope
    // NOTE: Not referring variableScope. It is intended.
    // Since
    //  in ES5, FunctionDeclaration should be in FunctionBody.
    //  in ES6, FunctionDeclaration should be block scoped.

    if (node.type === AST_NODE_TYPES.FunctionExpression) {
      if (node.id) {
        // FunctionExpression with name creates its special scope;
        // FunctionExpressionNameScope.
        this.scopeManager.nestFunctionExpressionNameScope(node);
      }
    } else if (node.id) {
      // id is defined in upper scope
      this.currentScope().defineIdentifier(
        node.id,
        new FunctionNameDefinition(node.id, node),
      );
    }

    // Consider this function is in the MethodDefinition.
    this.scopeManager.nestFunctionScope(node, false);

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
      param.decorators.forEach(d => this.visit(d));
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    // In TypeScript there are a number of function-like constructs which have no body,
    // so check it exists before traversing
    if (node.body) {
      // Skip BlockStatement to prevent creating BlockStatement scope.
      if (node.body.type === AST_NODE_TYPES.BlockStatement) {
        this.visitChildren(node.body);
      } else {
        this.visit(node.body);
      }
    }

    this.close(node);
  }
```
</details>

##### `visitFunctionParameterTypeAnnotation(node: TSESTree.Parameter): void`

<details><summary>Code</summary>

```ts
protected visitFunctionParameterTypeAnnotation(
    node: TSESTree.Parameter,
  ): void {
    switch (node.type) {
      case AST_NODE_TYPES.AssignmentPattern:
        this.visitType(node.left.typeAnnotation);
        break;
      case AST_NODE_TYPES.TSParameterProperty:
        this.visitFunctionParameterTypeAnnotation(node.parameter);
        break;
      default:
        this.visitType(node.typeAnnotation);
        break;
    }
  }
```
</details>

##### `visitJSXElement(node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement): void`

<details><summary>Code</summary>

```ts
protected visitJSXElement(
    node: TSESTree.JSXClosingElement | TSESTree.JSXOpeningElement,
  ): void {
    if (node.name.type === AST_NODE_TYPES.JSXIdentifier) {
      if (
        node.name.name[0].toUpperCase() === node.name.name[0] ||
        node.name.name === 'this'
      ) {
        // lower cased component names are always treated as "intrinsic" names, and are converted to a string,
        // not a variable by JSX transforms:
        // <div /> => React.createElement("div", null)

        // the only case we want to visit a lower-cased component has its name as "this",
        this.visit(node.name);
      }
    } else {
      this.visit(node.name);
    }
  }
```
</details>

##### `visitProperty(node: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected visitProperty(node: TSESTree.Property): void {
    if (node.computed) {
      this.visit(node.key);
    }

    this.visit(node.value);
  }
```
</details>

##### `visitType(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
protected visitType(node: TSESTree.Node | null | undefined): void {
    if (!node) {
      return;
    }
    TypeVisitor.visit(this, node);
  }
```
</details>

##### `visitTypeAssertion(node: | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion): void`

<details><summary>Code</summary>

```ts
protected visitTypeAssertion(
    node:
      | TSESTree.TSAsExpression
      | TSESTree.TSSatisfiesExpression
      | TSESTree.TSTypeAssertion,
  ): void {
    this.visit(node.expression);
    this.visitType(node.typeAnnotation);
  }
```
</details>

##### `ArrowFunctionExpression(node: TSESTree.ArrowFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected ArrowFunctionExpression(
    node: TSESTree.ArrowFunctionExpression,
  ): void {
    this.visitFunction(node);
  }
```
</details>

##### `AssignmentExpression(node: TSESTree.AssignmentExpression): void`

<details><summary>Code</summary>

```ts
protected AssignmentExpression(node: TSESTree.AssignmentExpression): void {
    const left = this.visitExpressionTarget(node.left);

    if (PatternVisitor.isPattern(left)) {
      if (node.operator === '=') {
        this.visitPattern(
          left,
          (pattern, info) => {
            const maybeImplicitGlobal = !this.currentScope().isStrict
              ? {
                  node,
                  pattern,
                }
              : null;
            this.referencingDefaultValue(
              pattern,
              info.assignments,
              maybeImplicitGlobal,
              false,
            );
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              node.right,
              maybeImplicitGlobal,
              false,
            );
          },
          { processRightHandNodes: true },
        );
      } else if (left.type === AST_NODE_TYPES.Identifier) {
        this.currentScope().referenceValue(
          left,
          ReferenceFlag.ReadWrite,
          node.right,
        );
      }
    } else {
      this.visit(left);
    }
    this.visit(node.right);
  }
```
</details>

##### `BlockStatement(node: TSESTree.BlockStatement): void`

<details><summary>Code</summary>

```ts
protected BlockStatement(node: TSESTree.BlockStatement): void {
    this.scopeManager.nestBlockScope(node);

    this.visitChildren(node);

    this.close(node);
  }
```
</details>

##### `BreakStatement(): void`

<details><summary>Code</summary>

```ts
protected BreakStatement(): void {
    // don't reference the break statement's label
  }
```
</details>

##### `CallExpression(node: TSESTree.CallExpression): void`

<details><summary>Code</summary>

```ts
protected CallExpression(node: TSESTree.CallExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

##### `CatchClause(node: TSESTree.CatchClause): void`

<details><summary>Code</summary>

```ts
protected CatchClause(node: TSESTree.CatchClause): void {
    this.scopeManager.nestCatchScope(node);

    if (node.param) {
      const param = node.param;
      this.visitPattern(
        param,
        (pattern, info) => {
          this.currentScope().defineIdentifier(
            pattern,
            new CatchClauseDefinition(param, node),
          );
          this.referencingDefaultValue(pattern, info.assignments, null, true);
        },
        { processRightHandNodes: true },
      );
    }
    this.visit(node.body);

    this.close(node);
  }
```
</details>

##### `ClassDeclaration(node: TSESTree.ClassDeclaration): void`

<details><summary>Code</summary>

```ts
protected ClassDeclaration(node: TSESTree.ClassDeclaration): void {
    this.visitClass(node);
  }
```
</details>

##### `ClassExpression(node: TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected ClassExpression(node: TSESTree.ClassExpression): void {
    this.visitClass(node);
  }
```
</details>

##### `ContinueStatement(): void`

<details><summary>Code</summary>

```ts
protected ContinueStatement(): void {
    // don't reference the continue statement's label
  }
```
</details>

##### `ExportAllDeclaration(): void`

<details><summary>Code</summary>

```ts
protected ExportAllDeclaration(): void {
    // this defines no local variables
  }
```
</details>

##### `ExportDefaultDeclaration(node: TSESTree.ExportDefaultDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportDefaultDeclaration(
    node: TSESTree.ExportDefaultDeclaration,
  ): void {
    if (node.declaration.type === AST_NODE_TYPES.Identifier) {
      ExportVisitor.visit(this, node);
    } else {
      this.visit(node.declaration);
    }
  }
```
</details>

##### `ExportNamedDeclaration(node: TSESTree.ExportNamedDeclaration): void`

<details><summary>Code</summary>

```ts
protected ExportNamedDeclaration(
    node: TSESTree.ExportNamedDeclaration,
  ): void {
    if (node.declaration) {
      this.visit(node.declaration);
    } else {
      ExportVisitor.visit(this, node);
    }
  }
```
</details>

##### `ForInStatement(node: TSESTree.ForInStatement): void`

<details><summary>Code</summary>

```ts
protected ForInStatement(node: TSESTree.ForInStatement): void {
    this.visitForIn(node);
  }
```
</details>

##### `ForOfStatement(node: TSESTree.ForOfStatement): void`

<details><summary>Code</summary>

```ts
protected ForOfStatement(node: TSESTree.ForOfStatement): void {
    this.visitForIn(node);
  }
```
</details>

##### `ForStatement(node: TSESTree.ForStatement): void`

<details><summary>Code</summary>

```ts
protected ForStatement(node: TSESTree.ForStatement): void {
    // Create ForStatement declaration.
    // NOTE: In ES6, ForStatement dynamically generates per iteration environment. However, this is
    // a static analyzer, we only generate one scope for ForStatement.
    if (
      node.init &&
      node.init.type === AST_NODE_TYPES.VariableDeclaration &&
      node.init.kind !== 'var'
    ) {
      this.scopeManager.nestForScope(node);
    }

    this.visitChildren(node);

    this.close(node);
  }
```
</details>

##### `FunctionDeclaration(node: TSESTree.FunctionDeclaration): void`

<details><summary>Code</summary>

```ts
protected FunctionDeclaration(node: TSESTree.FunctionDeclaration): void {
    this.visitFunction(node);
  }
```
</details>

##### `FunctionExpression(node: TSESTree.FunctionExpression): void`

<details><summary>Code</summary>

```ts
protected FunctionExpression(node: TSESTree.FunctionExpression): void {
    this.visitFunction(node);
  }
```
</details>

##### `Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.currentScope().referenceValue(node);
    this.visitType(node.typeAnnotation);
  }
```
</details>

##### `ImportAttribute(): void`

<details><summary>Code</summary>

```ts
protected ImportAttribute(): void {
    // import assertions are module metadata and thus have no variables to reference
  }
```
</details>

##### `ImportDeclaration(node: TSESTree.ImportDeclaration): void`

<details><summary>Code</summary>

```ts
protected ImportDeclaration(node: TSESTree.ImportDeclaration): void {
    assert(
      this.scopeManager.isModule(),
      'ImportDeclaration should appear when the mode is ES6 and in the module context.',
    );

    ImportVisitor.visit(this, node);
  }
```
</details>

##### `JSXAttribute(node: TSESTree.JSXAttribute): void`

<details><summary>Code</summary>

```ts
protected JSXAttribute(node: TSESTree.JSXAttribute): void {
    this.visit(node.value);
  }
```
</details>

##### `JSXClosingElement(node: TSESTree.JSXClosingElement): void`

<details><summary>Code</summary>

```ts
protected JSXClosingElement(node: TSESTree.JSXClosingElement): void {
    this.visitJSXElement(node);
  }
```
</details>

##### `JSXFragment(node: TSESTree.JSXFragment): void`

<details><summary>Code</summary>

```ts
protected JSXFragment(node: TSESTree.JSXFragment): void {
    this.referenceJsxPragma();
    this.referenceJsxFragment();
    this.visitChildren(node);
  }
```
</details>

##### `JSXIdentifier(node: TSESTree.JSXIdentifier): void`

<details><summary>Code</summary>

```ts
protected JSXIdentifier(node: TSESTree.JSXIdentifier): void {
    this.currentScope().referenceValue(node);
  }
```
</details>

##### `JSXMemberExpression(node: TSESTree.JSXMemberExpression): void`

<details><summary>Code</summary>

```ts
protected JSXMemberExpression(node: TSESTree.JSXMemberExpression): void {
    if (
      node.object.type !== AST_NODE_TYPES.JSXIdentifier ||
      node.object.name !== 'this'
    ) {
      this.visit(node.object);
    }
    // we don't ever reference the property as it's always going to be a property on the thing
  }
```
</details>

##### `JSXOpeningElement(node: TSESTree.JSXOpeningElement): void`

<details><summary>Code</summary>

```ts
protected JSXOpeningElement(node: TSESTree.JSXOpeningElement): void {
    this.referenceJsxPragma();
    this.visitJSXElement(node);
    this.visitType(node.typeArguments);
    for (const attr of node.attributes) {
      this.visit(attr);
    }
  }
```
</details>

##### `LabeledStatement(node: TSESTree.LabeledStatement): void`

<details><summary>Code</summary>

```ts
protected LabeledStatement(node: TSESTree.LabeledStatement): void {
    this.visit(node.body);
  }
```
</details>

##### `MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    if (node.computed) {
      this.visit(node.property);
    }
  }
```
</details>

##### `MetaProperty(): void`

<details><summary>Code</summary>

```ts
protected MetaProperty(): void {
    // meta properties all builtin globals
  }
```
</details>

##### `NewExpression(node: TSESTree.NewExpression): void`

<details><summary>Code</summary>

```ts
protected NewExpression(node: TSESTree.NewExpression): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

##### `PrivateIdentifier(): void`

<details><summary>Code</summary>

```ts
protected PrivateIdentifier(): void {
    // private identifiers are members on classes and thus have no variables to reference
  }
```
</details>

##### `Program(node: TSESTree.Program): void`

<details><summary>Code</summary>

```ts
protected Program(node: TSESTree.Program): void {
    const globalScope = this.scopeManager.nestGlobalScope(node);
    this.populateGlobalsFromLib(globalScope);

    if (this.scopeManager.isGlobalReturn()) {
      // Force strictness of GlobalScope to false when using node.js scope.
      this.currentScope().isStrict = false;
      this.scopeManager.nestFunctionScope(node, false);
    }

    if (this.scopeManager.isModule()) {
      this.scopeManager.nestModuleScope(node);
    }

    if (this.scopeManager.isImpliedStrict()) {
      this.currentScope().isStrict = true;
    }

    this.visitChildren(node);
    this.close(node);
  }
```
</details>

##### `Property(node: TSESTree.Property): void`

<details><summary>Code</summary>

```ts
protected Property(node: TSESTree.Property): void {
    this.visitProperty(node);
  }
```
</details>

##### `SwitchStatement(node: TSESTree.SwitchStatement): void`

<details><summary>Code</summary>

```ts
protected SwitchStatement(node: TSESTree.SwitchStatement): void {
    this.visit(node.discriminant);

    this.scopeManager.nestSwitchScope(node);

    for (const switchCase of node.cases) {
      this.visit(switchCase);
    }

    this.close(node);
  }
```
</details>

##### `TaggedTemplateExpression(node: TSESTree.TaggedTemplateExpression): void`

<details><summary>Code</summary>

```ts
protected TaggedTemplateExpression(
    node: TSESTree.TaggedTemplateExpression,
  ): void {
    this.visit(node.tag);
    this.visit(node.quasi);
    this.visitType(node.typeArguments);
  }
```
</details>

##### `TSAsExpression(node: TSESTree.TSAsExpression): void`

<details><summary>Code</summary>

```ts
protected TSAsExpression(node: TSESTree.TSAsExpression): void {
    this.visitTypeAssertion(node);
  }
```
</details>

##### `TSDeclareFunction(node: TSESTree.TSDeclareFunction): void`

<details><summary>Code</summary>

```ts
protected TSDeclareFunction(node: TSESTree.TSDeclareFunction): void {
    this.visitFunction(node);
  }
```
</details>

##### `TSEmptyBodyFunctionExpression(node: TSESTree.TSEmptyBodyFunctionExpression): void`

<details><summary>Code</summary>

```ts
protected TSEmptyBodyFunctionExpression(
    node: TSESTree.TSEmptyBodyFunctionExpression,
  ): void {
    this.visitFunction(node);
  }
```
</details>

##### `TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSEnumDeclaration(node: TSESTree.TSEnumDeclaration): void {
    this.currentScope().defineIdentifier(
      node.id,
      new TSEnumNameDefinition(node.id, node),
    );

    // enum members can be referenced within the enum body
    this.scopeManager.nestTSEnumScope(node);

    for (const member of node.body.members) {
      // TS resolves literal named members to be actual names
      // enum Foo {
      //   'a' = 1,
      //   b = a, // this references the 'a' member
      // }
      if (
        member.id.type === AST_NODE_TYPES.Literal &&
        typeof member.id.value === 'string'
      ) {
        const name = member.id;
        this.currentScope().defineLiteralIdentifier(
          name,
          new TSEnumMemberDefinition(name, member),
        );
      } else if (
        !member.computed &&
        member.id.type === AST_NODE_TYPES.Identifier
      ) {
        this.currentScope().defineIdentifier(
          member.id,
          new TSEnumMemberDefinition(member.id, member),
        );
      }

      this.visit(member.initializer);
    }

    this.close(node);
  }
```
</details>

##### `TSExportAssignment(node: TSESTree.TSExportAssignment): void`

<details><summary>Code</summary>

```ts
protected TSExportAssignment(node: TSESTree.TSExportAssignment): void {
    if (node.expression.type === AST_NODE_TYPES.Identifier) {
      // this is a special case - you can `export = T` where `T` is a type OR a
      // value however `T[U]` is illegal when `T` is a type and `T.U` is illegal
      // when `T.U` is a type
      // i.e. if the expression is JUST an Identifier - it could be either ref
      // kind; otherwise the standard rules apply
      this.currentScope().referenceDualValueType(node.expression);
    } else {
      this.visit(node.expression);
    }
  }
```
</details>

##### `TSImportEqualsDeclaration(node: TSESTree.TSImportEqualsDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSImportEqualsDeclaration(
    node: TSESTree.TSImportEqualsDeclaration,
  ): void {
    this.currentScope().defineIdentifier(
      node.id,
      new ImportBindingDefinition(node.id, node, node),
    );

    if (node.moduleReference.type === AST_NODE_TYPES.TSQualifiedName) {
      let moduleIdentifier = node.moduleReference.left;
      while (moduleIdentifier.type === AST_NODE_TYPES.TSQualifiedName) {
        moduleIdentifier = moduleIdentifier.left;
      }
      this.visit(moduleIdentifier);
    } else {
      this.visit(node.moduleReference);
    }
  }
```
</details>

##### `TSInstantiationExpression(node: TSESTree.TSInstantiationExpression): void`

<details><summary>Code</summary>

```ts
protected TSInstantiationExpression(
    node: TSESTree.TSInstantiationExpression,
  ): void {
    this.visitChildren(node, ['typeArguments']);
    this.visitType(node.typeArguments);
  }
```
</details>

##### `TSInterfaceDeclaration(node: TSESTree.TSInterfaceDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.visitType(node);
  }
```
</details>

##### `TSModuleDeclaration(node: TSESTree.TSModuleDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSModuleDeclaration(node: TSESTree.TSModuleDeclaration): void {
    if (node.id.type === AST_NODE_TYPES.Identifier && node.kind !== 'global') {
      this.currentScope().defineIdentifier(
        node.id,
        new TSModuleNameDefinition(node.id, node),
      );
    }

    this.scopeManager.nestTSModuleScope(node);

    this.visit(node.body);

    this.close(node);
  }
```
</details>

##### `TSSatisfiesExpression(node: TSESTree.TSSatisfiesExpression): void`

<details><summary>Code</summary>

```ts
protected TSSatisfiesExpression(node: TSESTree.TSSatisfiesExpression): void {
    this.visitTypeAssertion(node);
  }
```
</details>

##### `TSTypeAliasDeclaration(node: TSESTree.TSTypeAliasDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.visitType(node);
  }
```
</details>

##### `TSTypeAssertion(node: TSESTree.TSTypeAssertion): void`

<details><summary>Code</summary>

```ts
protected TSTypeAssertion(node: TSESTree.TSTypeAssertion): void {
    this.visitTypeAssertion(node);
  }
```
</details>

##### `UpdateExpression(node: TSESTree.UpdateExpression): void`

<details><summary>Code</summary>

```ts
protected UpdateExpression(node: TSESTree.UpdateExpression): void {
    const argument = this.visitExpressionTarget(node.argument);

    if (PatternVisitor.isPattern(argument)) {
      this.visitPattern(argument, pattern => {
        this.currentScope().referenceValue(
          pattern,
          ReferenceFlag.ReadWrite,
          null,
        );
      });
    } else {
      this.visitChildren(node);
    }
  }
```
</details>

##### `VariableDeclaration(node: TSESTree.VariableDeclaration): void`

<details><summary>Code</summary>

```ts
protected VariableDeclaration(node: TSESTree.VariableDeclaration): void {
    const variableTargetScope =
      node.kind === 'var'
        ? this.currentScope().variableScope
        : this.currentScope();

    for (const decl of node.declarations) {
      const init = decl.init;

      this.visitPattern(
        decl.id,
        (pattern, info) => {
          variableTargetScope.defineIdentifier(
            pattern,
            new VariableDefinition(pattern, decl, node),
          );

          this.referencingDefaultValue(pattern, info.assignments, null, true);
          if (init) {
            this.currentScope().referenceValue(
              pattern,
              ReferenceFlag.Write,
              init,
              null,
              true,
            );
          }
        },
        { processRightHandNodes: true },
      );

      this.visit(decl.init);
      this.visitType(decl.id.typeAnnotation);
    }
  }
```
</details>

##### `WithStatement(node: TSESTree.WithStatement): void`

<details><summary>Code</summary>

```ts
protected WithStatement(node: TSESTree.WithStatement): void {
    this.visit(node.object);

    // Then nest scope for WithStatement.
    this.scopeManager.nestWithScope(node);

    this.visit(node.body);

    this.close(node);
  }
```
</details>

##### `visitExpressionTarget(left: TSESTree.Node): TSESTree.Node`

<details><summary>Code</summary>

```ts
private visitExpressionTarget(left: TSESTree.Node) {
    switch (left.type) {
      case AST_NODE_TYPES.TSAsExpression:
      case AST_NODE_TYPES.TSTypeAssertion:
        // explicitly visit the type annotation
        this.visitType(left.typeAnnotation);
      // intentional fallthrough
      case AST_NODE_TYPES.TSNonNullExpression:
        // unwrap the expression
        left = left.expression;
    }

    return left;
  }
```
</details>


---

## Interfaces

### `ReferencerOptions`

<details><summary>Interface Code</summary>

```ts
export interface ReferencerOptions extends VisitorOptions {
  jsxFragmentName: string | null;
  jsxPragma: string | null;
  lib: Lib[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `jsxFragmentName` | `string | null` | ✗ |  |
| `jsxPragma` | `string | null` | ✗ |  |
| `lib` | `Lib[]` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---