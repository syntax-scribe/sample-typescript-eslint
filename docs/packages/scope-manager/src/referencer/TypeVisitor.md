[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TypeVisitor.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 24
- **Classes**: 1
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/TypeVisitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Scope` | `../scope` |
| `Referencer` | `./Referencer` |
| `ParameterDefinition` | `../definition` |
| `TypeDefinition` | `../definition` |
| `ScopeType` | `../scope` |
| `Visitor` | `./Visitor` |


---

## Functions

### `TypeVisitor.visit(referencer: Referencer, node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
static visit(referencer: Referencer, node: TSESTree.Node): void {
    const typeReferencer = new TypeVisitor(referencer);
    typeReferencer.visit(node);
  }
```
</details>

- **Parameters**:
  - `referencer: Referencer`
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `typeReferencer.visit`
### `TypeVisitor.visitFunctionType(node: | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature): void`

<details><summary>Code</summary>

```ts
protected visitFunctionType(
    node:
      | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature,
  ): void {
    // arguments and type parameters can only be referenced from within the function
    this.#referencer.scopeManager.nestFunctionTypeScope(node);
    this.visit(node.typeParameters);

    for (const param of node.params) {
      let didVisitAnnotation = false;
      this.visitPattern(param, (pattern, info) => {
        // a parameter name creates a value type variable which can be referenced later via typeof arg
        this.#referencer
          .currentScope()
          .defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

        if (pattern.typeAnnotation) {
          this.visit(pattern.typeAnnotation);
          didVisitAnnotation = true;
        }
      });

      // there are a few special cases where the type annotation is owned by the parameter, not the pattern
      // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
      if (!didVisitAnnotation && 'typeAnnotation' in param) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.returnType);

    this.#referencer.close(node);
  }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.scopeManager.nestFunctionTypeScope`
  - `this.visit`
  - `this.visitPattern`
  - `this.#referencer
          .currentScope()
          .defineIdentifier`
  - `this.#referencer.close`
- **Internal Comments**:
```
// arguments and type parameters can only be referenced from within the function (x6)
// a parameter name creates a value type variable which can be referenced later via typeof arg (x7)
// there are a few special cases where the type annotation is owned by the parameter, not the pattern
// eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
```

### `TypeVisitor.visitPropertyKey(node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature): void`

<details><summary>Code</summary>

```ts
protected visitPropertyKey(
    node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature,
  ): void {
    if (!node.computed) {
      return;
    }
    // computed members are treated as value references, and TS expects they have a literal type
    this.#referencer.visit(node.key);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.visit`
- **Internal Comments**:
```
// computed members are treated as value references, and TS expects they have a literal type (x5)
```

### `TypeVisitor.Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.currentScope().referenceType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.currentScope().referenceType`
### `TypeVisitor.MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    // don't visit the property
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `TypeVisitor.TSCallSignatureDeclaration(node: TSESTree.TSCallSignatureDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSCallSignatureDeclaration(
    node: TSESTree.TSCallSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSCallSignatureDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunctionType`
### `TypeVisitor.TSConditionalType(node: TSESTree.TSConditionalType): void`

<details><summary>Code</summary>

```ts
protected TSConditionalType(node: TSESTree.TSConditionalType): void {
    // conditional types can define inferred type parameters
    // which are only accessible from inside the conditional parameter
    this.#referencer.scopeManager.nestConditionalTypeScope(node);

    // type parameters inferred in the condition clause are not accessible within the false branch
    this.visitChildren(node, ['falseType']);

    this.#referencer.close(node);

    this.visit(node.falseType);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSConditionalType`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.scopeManager.nestConditionalTypeScope`
  - `this.visitChildren`
  - `this.#referencer.close`
  - `this.visit`
- **Internal Comments**:
```
// conditional types can define inferred type parameters (x6)
// which are only accessible from inside the conditional parameter (x6)
// type parameters inferred in the condition clause are not accessible within the false branch (x4)
```

### `TypeVisitor.TSConstructorType(node: TSESTree.TSConstructorType): void`

<details><summary>Code</summary>

```ts
protected TSConstructorType(node: TSESTree.TSConstructorType): void {
    this.visitFunctionType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSConstructorType`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunctionType`
### `TypeVisitor.TSConstructSignatureDeclaration(node: TSESTree.TSConstructSignatureDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSConstructSignatureDeclaration(
    node: TSESTree.TSConstructSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSConstructSignatureDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunctionType`
### `TypeVisitor.TSFunctionType(node: TSESTree.TSFunctionType): void`

<details><summary>Code</summary>

```ts
protected TSFunctionType(node: TSESTree.TSFunctionType): void {
    this.visitFunctionType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSFunctionType`
- **Return Type**: `void`
- **Calls**:
  - `this.visitFunctionType`
### `TypeVisitor.TSImportType(node: TSESTree.TSImportType): void`

<details><summary>Code</summary>

```ts
protected TSImportType(node: TSESTree.TSImportType): void {
    // the TS parser allows any type to be the parameter, but it's a syntax error - so we can ignore it
    this.visit(node.typeArguments);
    // the qualifier is just part of a standard EntityName, so it should not be visited
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSImportType`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
- **Internal Comments**:
```
// the TS parser allows any type to be the parameter, but it's a syntax error - so we can ignore it (x4)
```

### `TypeVisitor.TSIndexSignature(node: TSESTree.TSIndexSignature): void`

<details><summary>Code</summary>

```ts
protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    for (const param of node.parameters) {
      if (param.type === AST_NODE_TYPES.Identifier) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSIndexSignature`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `TypeVisitor.TSInferType(node: TSESTree.TSInferType): void`

<details><summary>Code</summary>

```ts
protected TSInferType(node: TSESTree.TSInferType): void {
    const typeParameter = node.typeParameter;
    let scope = this.#referencer.currentScope();

    /*
    In cases where there is a sub-type scope created within a conditional type, then the generic should be defined in the
    conditional type's scope, not the child type scope.
    If we define it within the child type's scope then it won't be able to be referenced outside the child type
    */
    if (
      scope.type === ScopeType.functionType ||
      scope.type === ScopeType.mappedType
    ) {
      // search up the scope tree to figure out if we're in a nested type scope
      let currentScope = scope.upper as Scope | undefined;
      while (currentScope) {
        if (
          currentScope.type === ScopeType.functionType ||
          currentScope.type === ScopeType.mappedType
        ) {
          // ensure valid type parents only
          currentScope = currentScope.upper;
          continue;
        }
        if (currentScope.type === ScopeType.conditionalType) {
          scope = currentScope;
          break;
        }
        break;
      }
    }

    scope.defineIdentifier(
      typeParameter.name,
      new TypeDefinition(typeParameter.name, typeParameter),
    );

    this.visit(typeParameter.constraint);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSInferType`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.currentScope`
  - `scope.defineIdentifier`
  - `this.visit`
- **Internal Comments**:
```
/*
    In cases where there is a sub-type scope created within a conditional type, then the generic should be defined in the
    conditional type's scope, not the child type scope.
    If we define it within the child type's scope then it won't be able to be referenced outside the child type
    */
// search up the scope tree to figure out if we're in a nested type scope (x2)
// ensure valid type parents only (x3)
```

### `TypeVisitor.TSInterfaceDeclaration(node: TSESTree.TSInterfaceDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    node.extends.forEach(this.visit, this);
    this.visit(node.body);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSInterfaceDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer
      .currentScope()
      .defineIdentifier`
  - `this.#referencer.scopeManager.nestTypeScope`
  - `this.visit`
  - `node.extends.forEach`
  - `this.#referencer.close`
- **Internal Comments**:
```
// type parameters cannot be referenced from outside their current scope (x6)
```

### `TypeVisitor.TSMappedType(node: TSESTree.TSMappedType): void`

<details><summary>Code</summary>

```ts
protected TSMappedType(node: TSESTree.TSMappedType): void {
    // mapped types key can only be referenced within their return value
    this.#referencer.scopeManager.nestMappedTypeScope(node);
    this.#referencer
      .currentScope()
      .defineIdentifier(node.key, new TypeDefinition(node.key, node));
    this.visit(node.constraint);
    this.visit(node.nameType);
    this.visit(node.typeAnnotation);
    this.#referencer.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSMappedType`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.scopeManager.nestMappedTypeScope`
  - `this.#referencer
      .currentScope()
      .defineIdentifier`
  - `this.visit`
  - `this.#referencer.close`
- **Internal Comments**:
```
// mapped types key can only be referenced within their return value (x6)
```

### `TypeVisitor.TSMethodSignature(node: TSESTree.TSMethodSignature): void`

<details><summary>Code</summary>

```ts
protected TSMethodSignature(node: TSESTree.TSMethodSignature): void {
    this.visitPropertyKey(node);
    this.visitFunctionType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSMethodSignature`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyKey`
  - `this.visitFunctionType`
### `TypeVisitor.TSNamedTupleMember(node: TSESTree.TSNamedTupleMember): void`

<details><summary>Code</summary>

```ts
protected TSNamedTupleMember(node: TSESTree.TSNamedTupleMember): void {
    this.visit(node.elementType);
    // we don't visit the label as the label only exists for the purposes of documentation
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSNamedTupleMember`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `TypeVisitor.TSPropertySignature(node: TSESTree.TSPropertySignature): void`

<details><summary>Code</summary>

```ts
protected TSPropertySignature(node: TSESTree.TSPropertySignature): void {
    this.visitPropertyKey(node);
    this.visit(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignature`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyKey`
  - `this.visit`
### `TypeVisitor.TSQualifiedName(node: TSESTree.TSQualifiedName): void`

<details><summary>Code</summary>

```ts
protected TSQualifiedName(node: TSESTree.TSQualifiedName): void {
    this.visit(node.left);
    // we don't visit the right as it a name on the thing, not a name to reference
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSQualifiedName`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
### `TypeVisitor.TSTypeAliasDeclaration(node: TSESTree.TSTypeAliasDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    this.visit(node.typeAnnotation);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeAliasDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer
      .currentScope()
      .defineIdentifier`
  - `this.#referencer.scopeManager.nestTypeScope`
  - `this.visit`
  - `this.#referencer.close`
- **Internal Comments**:
```
// type parameters cannot be referenced from outside their current scope (x6)
```

### `TypeVisitor.TSTypeParameter(node: TSESTree.TSTypeParameter): void`

<details><summary>Code</summary>

```ts
protected TSTypeParameter(node: TSESTree.TSTypeParameter): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.name, new TypeDefinition(node.name, node));

    this.visit(node.constraint);
    this.visit(node.default);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer
      .currentScope()
      .defineIdentifier`
  - `this.visit`
### `TypeVisitor.TSTypePredicate(node: TSESTree.TSTypePredicate): void`

<details><summary>Code</summary>

```ts
protected TSTypePredicate(node: TSESTree.TSTypePredicate): void {
    if (node.parameterName.type !== AST_NODE_TYPES.TSThisType) {
      this.#referencer.currentScope().referenceValue(node.parameterName);
    }
    this.visit(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypePredicate`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.currentScope().referenceValue`
  - `this.visit`
### `TypeVisitor.TSTypeAnnotation(node: TSESTree.TSTypeAnnotation): void`

<details><summary>Code</summary>

```ts
protected TSTypeAnnotation(node: TSESTree.TSTypeAnnotation): void {
    // check
    this.visitChildren(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeAnnotation`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
- **Internal Comments**:
```
// check (x4)
```

### `TypeVisitor.TSTypeQuery(node: TSESTree.TSTypeQuery): void`

<details><summary>Code</summary>

```ts
protected TSTypeQuery(node: TSESTree.TSTypeQuery): void {
    let entityName:
      | TSESTree.Identifier
      | TSESTree.ThisExpression
      | TSESTree.TSImportType;
    if (node.exprName.type === AST_NODE_TYPES.TSQualifiedName) {
      let iter = node.exprName;
      while (iter.left.type === AST_NODE_TYPES.TSQualifiedName) {
        iter = iter.left;
      }
      entityName = iter.left;
    } else {
      entityName = node.exprName;

      if (node.exprName.type === AST_NODE_TYPES.TSImportType) {
        this.visit(node.exprName);
      }
    }
    if (entityName.type === AST_NODE_TYPES.Identifier) {
      this.#referencer.currentScope().referenceValue(entityName);
    }

    this.visit(node.typeArguments);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeQuery`
- **Return Type**: `void`
- **Calls**:
  - `this.visit`
  - `this.#referencer.currentScope().referenceValue`

---

## Classes

### `TypeVisitor`

<details><summary>Class Code</summary>

```ts
export class TypeVisitor extends Visitor {
  readonly #referencer: Referencer;

  constructor(referencer: Referencer) {
    super(referencer);
    this.#referencer = referencer;
  }

  static visit(referencer: Referencer, node: TSESTree.Node): void {
    const typeReferencer = new TypeVisitor(referencer);
    typeReferencer.visit(node);
  }

  ///////////////////
  // Visit helpers //
  ///////////////////

  protected visitFunctionType(
    node:
      | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature,
  ): void {
    // arguments and type parameters can only be referenced from within the function
    this.#referencer.scopeManager.nestFunctionTypeScope(node);
    this.visit(node.typeParameters);

    for (const param of node.params) {
      let didVisitAnnotation = false;
      this.visitPattern(param, (pattern, info) => {
        // a parameter name creates a value type variable which can be referenced later via typeof arg
        this.#referencer
          .currentScope()
          .defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

        if (pattern.typeAnnotation) {
          this.visit(pattern.typeAnnotation);
          didVisitAnnotation = true;
        }
      });

      // there are a few special cases where the type annotation is owned by the parameter, not the pattern
      // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
      if (!didVisitAnnotation && 'typeAnnotation' in param) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.returnType);

    this.#referencer.close(node);
  }

  protected visitPropertyKey(
    node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature,
  ): void {
    if (!node.computed) {
      return;
    }
    // computed members are treated as value references, and TS expects they have a literal type
    this.#referencer.visit(node.key);
  }

  /////////////////////
  // Visit selectors //
  /////////////////////

  protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.currentScope().referenceType(node);
  }

  protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    // don't visit the property
  }

  protected TSCallSignatureDeclaration(
    node: TSESTree.TSCallSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }

  protected TSConditionalType(node: TSESTree.TSConditionalType): void {
    // conditional types can define inferred type parameters
    // which are only accessible from inside the conditional parameter
    this.#referencer.scopeManager.nestConditionalTypeScope(node);

    // type parameters inferred in the condition clause are not accessible within the false branch
    this.visitChildren(node, ['falseType']);

    this.#referencer.close(node);

    this.visit(node.falseType);
  }

  protected TSConstructorType(node: TSESTree.TSConstructorType): void {
    this.visitFunctionType(node);
  }

  protected TSConstructSignatureDeclaration(
    node: TSESTree.TSConstructSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }

  protected TSFunctionType(node: TSESTree.TSFunctionType): void {
    this.visitFunctionType(node);
  }

  protected TSImportType(node: TSESTree.TSImportType): void {
    // the TS parser allows any type to be the parameter, but it's a syntax error - so we can ignore it
    this.visit(node.typeArguments);
    // the qualifier is just part of a standard EntityName, so it should not be visited
  }

  protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    for (const param of node.parameters) {
      if (param.type === AST_NODE_TYPES.Identifier) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.typeAnnotation);
  }

  protected TSInferType(node: TSESTree.TSInferType): void {
    const typeParameter = node.typeParameter;
    let scope = this.#referencer.currentScope();

    /*
    In cases where there is a sub-type scope created within a conditional type, then the generic should be defined in the
    conditional type's scope, not the child type scope.
    If we define it within the child type's scope then it won't be able to be referenced outside the child type
    */
    if (
      scope.type === ScopeType.functionType ||
      scope.type === ScopeType.mappedType
    ) {
      // search up the scope tree to figure out if we're in a nested type scope
      let currentScope = scope.upper as Scope | undefined;
      while (currentScope) {
        if (
          currentScope.type === ScopeType.functionType ||
          currentScope.type === ScopeType.mappedType
        ) {
          // ensure valid type parents only
          currentScope = currentScope.upper;
          continue;
        }
        if (currentScope.type === ScopeType.conditionalType) {
          scope = currentScope;
          break;
        }
        break;
      }
    }

    scope.defineIdentifier(
      typeParameter.name,
      new TypeDefinition(typeParameter.name, typeParameter),
    );

    this.visit(typeParameter.constraint);
  }

  protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    node.extends.forEach(this.visit, this);
    this.visit(node.body);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }

  protected TSMappedType(node: TSESTree.TSMappedType): void {
    // mapped types key can only be referenced within their return value
    this.#referencer.scopeManager.nestMappedTypeScope(node);
    this.#referencer
      .currentScope()
      .defineIdentifier(node.key, new TypeDefinition(node.key, node));
    this.visit(node.constraint);
    this.visit(node.nameType);
    this.visit(node.typeAnnotation);
    this.#referencer.close(node);
  }

  protected TSMethodSignature(node: TSESTree.TSMethodSignature): void {
    this.visitPropertyKey(node);
    this.visitFunctionType(node);
  }

  protected TSNamedTupleMember(node: TSESTree.TSNamedTupleMember): void {
    this.visit(node.elementType);
    // we don't visit the label as the label only exists for the purposes of documentation
  }

  protected TSPropertySignature(node: TSESTree.TSPropertySignature): void {
    this.visitPropertyKey(node);
    this.visit(node.typeAnnotation);
  }

  protected TSQualifiedName(node: TSESTree.TSQualifiedName): void {
    this.visit(node.left);
    // we don't visit the right as it a name on the thing, not a name to reference
  }

  protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    this.visit(node.typeAnnotation);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }

  protected TSTypeParameter(node: TSESTree.TSTypeParameter): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.name, new TypeDefinition(node.name, node));

    this.visit(node.constraint);
    this.visit(node.default);
  }

  protected TSTypePredicate(node: TSESTree.TSTypePredicate): void {
    if (node.parameterName.type !== AST_NODE_TYPES.TSThisType) {
      this.#referencer.currentScope().referenceValue(node.parameterName);
    }
    this.visit(node.typeAnnotation);
  }

  // a type query `typeof foo` is a special case that references a _non-type_ variable,
  protected TSTypeAnnotation(node: TSESTree.TSTypeAnnotation): void {
    // check
    this.visitChildren(node);
  }

  protected TSTypeQuery(node: TSESTree.TSTypeQuery): void {
    let entityName:
      | TSESTree.Identifier
      | TSESTree.ThisExpression
      | TSESTree.TSImportType;
    if (node.exprName.type === AST_NODE_TYPES.TSQualifiedName) {
      let iter = node.exprName;
      while (iter.left.type === AST_NODE_TYPES.TSQualifiedName) {
        iter = iter.left;
      }
      entityName = iter.left;
    } else {
      entityName = node.exprName;

      if (node.exprName.type === AST_NODE_TYPES.TSImportType) {
        this.visit(node.exprName);
      }
    }
    if (entityName.type === AST_NODE_TYPES.Identifier) {
      this.#referencer.currentScope().referenceValue(entityName);
    }

    this.visit(node.typeArguments);
  }
}
```
</details>

#### Methods

##### `visit(referencer: Referencer, node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
static visit(referencer: Referencer, node: TSESTree.Node): void {
    const typeReferencer = new TypeVisitor(referencer);
    typeReferencer.visit(node);
  }
```
</details>

##### `visitFunctionType(node: | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature): void`

<details><summary>Code</summary>

```ts
protected visitFunctionType(
    node:
      | TSESTree.TSCallSignatureDeclaration
      | TSESTree.TSConstructorType
      | TSESTree.TSConstructSignatureDeclaration
      | TSESTree.TSFunctionType
      | TSESTree.TSMethodSignature,
  ): void {
    // arguments and type parameters can only be referenced from within the function
    this.#referencer.scopeManager.nestFunctionTypeScope(node);
    this.visit(node.typeParameters);

    for (const param of node.params) {
      let didVisitAnnotation = false;
      this.visitPattern(param, (pattern, info) => {
        // a parameter name creates a value type variable which can be referenced later via typeof arg
        this.#referencer
          .currentScope()
          .defineIdentifier(
            pattern,
            new ParameterDefinition(pattern, node, info.rest),
          );

        if (pattern.typeAnnotation) {
          this.visit(pattern.typeAnnotation);
          didVisitAnnotation = true;
        }
      });

      // there are a few special cases where the type annotation is owned by the parameter, not the pattern
      // eslint-disable-next-line @typescript-eslint/no-unnecessary-condition
      if (!didVisitAnnotation && 'typeAnnotation' in param) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.returnType);

    this.#referencer.close(node);
  }
```
</details>

##### `visitPropertyKey(node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature): void`

<details><summary>Code</summary>

```ts
protected visitPropertyKey(
    node: TSESTree.TSMethodSignature | TSESTree.TSPropertySignature,
  ): void {
    if (!node.computed) {
      return;
    }
    // computed members are treated as value references, and TS expects they have a literal type
    this.#referencer.visit(node.key);
  }
```
</details>

##### `Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.currentScope().referenceType(node);
  }
```
</details>

##### `MemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
protected MemberExpression(node: TSESTree.MemberExpression): void {
    this.visit(node.object);
    // don't visit the property
  }
```
</details>

##### `TSCallSignatureDeclaration(node: TSESTree.TSCallSignatureDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSCallSignatureDeclaration(
    node: TSESTree.TSCallSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }
```
</details>

##### `TSConditionalType(node: TSESTree.TSConditionalType): void`

<details><summary>Code</summary>

```ts
protected TSConditionalType(node: TSESTree.TSConditionalType): void {
    // conditional types can define inferred type parameters
    // which are only accessible from inside the conditional parameter
    this.#referencer.scopeManager.nestConditionalTypeScope(node);

    // type parameters inferred in the condition clause are not accessible within the false branch
    this.visitChildren(node, ['falseType']);

    this.#referencer.close(node);

    this.visit(node.falseType);
  }
```
</details>

##### `TSConstructorType(node: TSESTree.TSConstructorType): void`

<details><summary>Code</summary>

```ts
protected TSConstructorType(node: TSESTree.TSConstructorType): void {
    this.visitFunctionType(node);
  }
```
</details>

##### `TSConstructSignatureDeclaration(node: TSESTree.TSConstructSignatureDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSConstructSignatureDeclaration(
    node: TSESTree.TSConstructSignatureDeclaration,
  ): void {
    this.visitFunctionType(node);
  }
```
</details>

##### `TSFunctionType(node: TSESTree.TSFunctionType): void`

<details><summary>Code</summary>

```ts
protected TSFunctionType(node: TSESTree.TSFunctionType): void {
    this.visitFunctionType(node);
  }
```
</details>

##### `TSImportType(node: TSESTree.TSImportType): void`

<details><summary>Code</summary>

```ts
protected TSImportType(node: TSESTree.TSImportType): void {
    // the TS parser allows any type to be the parameter, but it's a syntax error - so we can ignore it
    this.visit(node.typeArguments);
    // the qualifier is just part of a standard EntityName, so it should not be visited
  }
```
</details>

##### `TSIndexSignature(node: TSESTree.TSIndexSignature): void`

<details><summary>Code</summary>

```ts
protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    for (const param of node.parameters) {
      if (param.type === AST_NODE_TYPES.Identifier) {
        this.visit(param.typeAnnotation);
      }
    }
    this.visit(node.typeAnnotation);
  }
```
</details>

##### `TSInferType(node: TSESTree.TSInferType): void`

<details><summary>Code</summary>

```ts
protected TSInferType(node: TSESTree.TSInferType): void {
    const typeParameter = node.typeParameter;
    let scope = this.#referencer.currentScope();

    /*
    In cases where there is a sub-type scope created within a conditional type, then the generic should be defined in the
    conditional type's scope, not the child type scope.
    If we define it within the child type's scope then it won't be able to be referenced outside the child type
    */
    if (
      scope.type === ScopeType.functionType ||
      scope.type === ScopeType.mappedType
    ) {
      // search up the scope tree to figure out if we're in a nested type scope
      let currentScope = scope.upper as Scope | undefined;
      while (currentScope) {
        if (
          currentScope.type === ScopeType.functionType ||
          currentScope.type === ScopeType.mappedType
        ) {
          // ensure valid type parents only
          currentScope = currentScope.upper;
          continue;
        }
        if (currentScope.type === ScopeType.conditionalType) {
          scope = currentScope;
          break;
        }
        break;
      }
    }

    scope.defineIdentifier(
      typeParameter.name,
      new TypeDefinition(typeParameter.name, typeParameter),
    );

    this.visit(typeParameter.constraint);
  }
```
</details>

##### `TSInterfaceDeclaration(node: TSESTree.TSInterfaceDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSInterfaceDeclaration(
    node: TSESTree.TSInterfaceDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    node.extends.forEach(this.visit, this);
    this.visit(node.body);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }
```
</details>

##### `TSMappedType(node: TSESTree.TSMappedType): void`

<details><summary>Code</summary>

```ts
protected TSMappedType(node: TSESTree.TSMappedType): void {
    // mapped types key can only be referenced within their return value
    this.#referencer.scopeManager.nestMappedTypeScope(node);
    this.#referencer
      .currentScope()
      .defineIdentifier(node.key, new TypeDefinition(node.key, node));
    this.visit(node.constraint);
    this.visit(node.nameType);
    this.visit(node.typeAnnotation);
    this.#referencer.close(node);
  }
```
</details>

##### `TSMethodSignature(node: TSESTree.TSMethodSignature): void`

<details><summary>Code</summary>

```ts
protected TSMethodSignature(node: TSESTree.TSMethodSignature): void {
    this.visitPropertyKey(node);
    this.visitFunctionType(node);
  }
```
</details>

##### `TSNamedTupleMember(node: TSESTree.TSNamedTupleMember): void`

<details><summary>Code</summary>

```ts
protected TSNamedTupleMember(node: TSESTree.TSNamedTupleMember): void {
    this.visit(node.elementType);
    // we don't visit the label as the label only exists for the purposes of documentation
  }
```
</details>

##### `TSPropertySignature(node: TSESTree.TSPropertySignature): void`

<details><summary>Code</summary>

```ts
protected TSPropertySignature(node: TSESTree.TSPropertySignature): void {
    this.visitPropertyKey(node);
    this.visit(node.typeAnnotation);
  }
```
</details>

##### `TSQualifiedName(node: TSESTree.TSQualifiedName): void`

<details><summary>Code</summary>

```ts
protected TSQualifiedName(node: TSESTree.TSQualifiedName): void {
    this.visit(node.left);
    // we don't visit the right as it a name on the thing, not a name to reference
  }
```
</details>

##### `TSTypeAliasDeclaration(node: TSESTree.TSTypeAliasDeclaration): void`

<details><summary>Code</summary>

```ts
protected TSTypeAliasDeclaration(
    node: TSESTree.TSTypeAliasDeclaration,
  ): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.id, new TypeDefinition(node.id, node));

    if (node.typeParameters) {
      // type parameters cannot be referenced from outside their current scope
      this.#referencer.scopeManager.nestTypeScope(node);
      this.visit(node.typeParameters);
    }

    this.visit(node.typeAnnotation);

    if (node.typeParameters) {
      this.#referencer.close(node);
    }
  }
```
</details>

##### `TSTypeParameter(node: TSESTree.TSTypeParameter): void`

<details><summary>Code</summary>

```ts
protected TSTypeParameter(node: TSESTree.TSTypeParameter): void {
    this.#referencer
      .currentScope()
      .defineIdentifier(node.name, new TypeDefinition(node.name, node));

    this.visit(node.constraint);
    this.visit(node.default);
  }
```
</details>

##### `TSTypePredicate(node: TSESTree.TSTypePredicate): void`

<details><summary>Code</summary>

```ts
protected TSTypePredicate(node: TSESTree.TSTypePredicate): void {
    if (node.parameterName.type !== AST_NODE_TYPES.TSThisType) {
      this.#referencer.currentScope().referenceValue(node.parameterName);
    }
    this.visit(node.typeAnnotation);
  }
```
</details>

##### `TSTypeAnnotation(node: TSESTree.TSTypeAnnotation): void`

<details><summary>Code</summary>

```ts
protected TSTypeAnnotation(node: TSESTree.TSTypeAnnotation): void {
    // check
    this.visitChildren(node);
  }
```
</details>

##### `TSTypeQuery(node: TSESTree.TSTypeQuery): void`

<details><summary>Code</summary>

```ts
protected TSTypeQuery(node: TSESTree.TSTypeQuery): void {
    let entityName:
      | TSESTree.Identifier
      | TSESTree.ThisExpression
      | TSESTree.TSImportType;
    if (node.exprName.type === AST_NODE_TYPES.TSQualifiedName) {
      let iter = node.exprName;
      while (iter.left.type === AST_NODE_TYPES.TSQualifiedName) {
        iter = iter.left;
      }
      entityName = iter.left;
    } else {
      entityName = node.exprName;

      if (node.exprName.type === AST_NODE_TYPES.TSImportType) {
        this.visit(node.exprName);
      }
    }
    if (entityName.type === AST_NODE_TYPES.Identifier) {
      this.#referencer.currentScope().referenceValue(entityName);
    }

    this.visit(node.typeArguments);
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