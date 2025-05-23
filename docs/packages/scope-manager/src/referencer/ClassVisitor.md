[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassVisitor.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 21
- **Classes**: 1
- **Imports**: 7
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/referencer/ClassVisitor.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `AST_NODE_TYPES` | `@typescript-eslint/types` |
| `Referencer` | `./Referencer` |
| `ClassNameDefinition` | `../definition` |
| `ParameterDefinition` | `../definition` |
| `TypeVisitor` | `./TypeVisitor` |
| `Visitor` | `./Visitor` |


---

## Functions

### `ClassVisitor.visit(referencer: Referencer, node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
static visit(
    referencer: Referencer,
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    const classVisitor = new ClassVisitor(referencer, node);
    classVisitor.visitClass(node);
  }
```
</details>

- **Parameters**:
  - `referencer: Referencer`
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
- **Return Type**: `void`
- **Calls**:
  - `classVisitor.visitClass`
### `ClassVisitor.visit(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
override visit(node: TSESTree.Node | null | undefined): void {
    // make sure we only handle the nodes we are designed to handle
    if (node && node.type in this) {
      super.visit(node);
    } else {
      this.#referencer.visit(node);
    }
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `super.visit`
  - `this.#referencer.visit`
- **Internal Comments**:
```
// make sure we only handle the nodes we are designed to handle
```

### `ClassVisitor.visitClass(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    if (node.type === AST_NODE_TYPES.ClassDeclaration && node.id) {
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    node.decorators.forEach(d => this.#referencer.visit(d));

    this.#referencer.scopeManager.nestClassScope(node);

    if (node.id) {
      // define the class name again inside the new scope
      // references to the class should not resolve directly to the parent class
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    this.#referencer.visit(node.superClass);

    // visit the type param declarations
    this.visitType(node.typeParameters);
    // then the usages
    this.visitType(node.superTypeArguments);
    node.implements.forEach(imp => this.visitType(imp));

    this.visit(node.body);

    this.#referencer.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer
        .currentScope()
        .defineIdentifier`
  - `node.decorators.forEach`
  - `this.#referencer.visit`
  - `this.#referencer.scopeManager.nestClassScope`
  - `this.visitType`
  - `node.implements.forEach`
  - `this.visit`
  - `this.#referencer.close`
- **Internal Comments**:
```
// define the class name again inside the new scope (x7)
// references to the class should not resolve directly to the parent class (x7)
// visit the type param declarations (x4)
// then the usages (x4)
```

### `ClassVisitor.visitFunctionParameterTypeAnnotation(node: TSESTree.Parameter): void`

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
### `ClassVisitor.visitMethod(node: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected visitMethod(node: TSESTree.MethodDefinition): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value.type === AST_NODE_TYPES.FunctionExpression) {
      this.visitMethodFunction(node.value, node);
    } else {
      this.#referencer.visit(node.value);
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.visit`
  - `this.visitMethodFunction`
  - `node.decorators.forEach`
### `ClassVisitor.visitMethodFunction(node: TSESTree.FunctionExpression, methodNode: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected visitMethodFunction(
    node: TSESTree.FunctionExpression,
    methodNode: TSESTree.MethodDefinition,
  ): void {
    if (node.id) {
      // FunctionExpression with name creates its special scope;
      // FunctionExpressionNameScope.
      this.#referencer.scopeManager.nestFunctionExpressionNameScope(node);
    }

    node.params.forEach(param => {
      param.decorators.forEach(d => this.visit(d));
    });

    // Consider this function is in the MethodDefinition.
    this.#referencer.scopeManager.nestFunctionScope(node, true);

    /**
     * class A {
     *   @meta     // <--- check this
     *   foo(a: Type) {}
     *
     *   @meta     // <--- check this
     *   foo(): Type {}
     * }
     */
    let withMethodDecorators = !!methodNode.decorators.length;
    /**
     * class A {
     *   foo(
     *     @meta    // <--- check this
     *     a: Type
     *   ) {}
     *
     *   set foo(
     *     @meta    // <--- EXCEPT this. TS do nothing for this
     *     a: Type
     *   ) {}
     * }
     */
    withMethodDecorators ||=
      methodNode.kind !== 'set' &&
      node.params.some(param => param.decorators.length);
    if (!withMethodDecorators && methodNode.kind === 'set') {
      const keyName = getLiteralMethodKeyName(methodNode);

      /**
       * class A {
       *   @meta      // <--- check this
       *   get a() {}
       *   set ['a'](v: Type) {}
       * }
       */
      if (
        keyName != null &&
        this.#classNode.body.body.find(
          (node): node is TSESTree.MethodDefinition =>
            node !== methodNode &&
            node.type === AST_NODE_TYPES.MethodDefinition &&
            // Node must both be static or not
            node.static === methodNode.static &&
            getLiteralMethodKeyName(node) === keyName,
        )?.decorators.length
      ) {
        withMethodDecorators = true;
      }
    }

    /**
     * @meta      // <--- check this
     * class A {
     *   constructor(a: Type) {}
     * }
     */
    if (
      !withMethodDecorators &&
      methodNode.kind === 'constructor' &&
      this.#classNode.decorators.length
    ) {
      withMethodDecorators = true;
    }

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.#referencer
            .currentScope()
            .defineIdentifier(
              pattern,
              new ParameterDefinition(pattern, node, info.rest),
            );

          this.#referencer.referencingDefaultValue(
            pattern,
            info.assignments,
            null,
            true,
          );
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    this.#referencer.visitChildren(node.body);
    this.#referencer.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.FunctionExpression`
  - `methodNode: TSESTree.MethodDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.scopeManager.nestFunctionExpressionNameScope`
  - `node.params.forEach`
  - `param.decorators.forEach`
  - `this.visit`
  - `this.#referencer.scopeManager.nestFunctionScope`
  - `node.params.some`
  - `getLiteralMethodKeyName`
  - `this.#classNode.body.body.find`
  - `this.visitPattern`
  - `this.#referencer
            .currentScope()
            .defineIdentifier`
  - `this.#referencer.referencingDefaultValue`
  - `this.visitFunctionParameterTypeAnnotation`
  - `this.visitType`
  - `this.#referencer.visitChildren`
  - `this.#referencer.close`
- **Internal Comments**:
```
// FunctionExpression with name creates its special scope; (x6)
// FunctionExpressionNameScope. (x6)
// Consider this function is in the MethodDefinition. (x6)
/**
     * class A {
     *   @meta     // <--- check this
     *   foo(a: Type) {}
     *
     *   @meta     // <--- check this
     *   foo(): Type {}
     * }
     */ (x2)
/**
     * class A {
     *   foo(
     *     @meta    // <--- check this
     *     a: Type
     *   ) {}
     *
     *   set foo(
     *     @meta    // <--- EXCEPT this. TS do nothing for this
     *     a: Type
     *   ) {}
     * }
     */ (x3)
/**
       * class A {
       *   @meta      // <--- check this
       *   get a() {}
       *   set ['a'](v: Type) {}
       * }
       */
// Node must both be static or not (x3)
/**
     * @meta      // <--- check this
     * class A {
     *   constructor(a: Type) {}
     * }
     */
// Process parameter declarations.
```

### `ClassVisitor.visitPropertyBase(node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected visitPropertyBase(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value) {
      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.scopeManager.nestClassFieldInitializerScope(
          node.value,
        );
      }

      this.#referencer.visit(node.value);

      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.close(node.value);
      }
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }
```
</details>

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.visit`
  - `this.#referencer.scopeManager.nestClassFieldInitializerScope`
  - `this.#referencer.close`
  - `node.decorators.forEach`
### `ClassVisitor.visitPropertyDefinition(node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected visitPropertyDefinition(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyBase(node);
    /**
     * class A {
     *   @meta     // <--- check this
     *   foo: Type;
     * }
     */
    this.visitType(node.typeAnnotation);
  }
```
</details>

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyBase`
  - `this.visitType`
- **Internal Comments**:
```
/**
     * class A {
     *   @meta     // <--- check this
     *   foo: Type;
     * }
     */ (x4)
```

### `ClassVisitor.visitType(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
protected visitType(node: TSESTree.Node | null | undefined): void {
    if (!node) {
      return;
    }
    TypeVisitor.visit(this.#referencer, node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | null | undefined`
- **Return Type**: `void`
- **Calls**:
  - `TypeVisitor.visit`
### `ClassVisitor.AccessorProperty(node: TSESTree.AccessorProperty): void`

<details><summary>Code</summary>

```ts
protected AccessorProperty(node: TSESTree.AccessorProperty): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorProperty`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyDefinition`
### `ClassVisitor.ClassBody(node: TSESTree.ClassBody): void`

<details><summary>Code</summary>

```ts
protected ClassBody(node: TSESTree.ClassBody): void {
    // this is here on purpose so that this visitor explicitly declares visitors
    // for all nodes it cares about (see the instance visit method above)
    this.visitChildren(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassBody`
- **Return Type**: `void`
- **Calls**:
  - `this.visitChildren`
- **Internal Comments**:
```
// this is here on purpose so that this visitor explicitly declares visitors (x4)
// for all nodes it cares about (see the instance visit method above) (x4)
```

### `ClassVisitor.Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.visit(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.visit`
### `ClassVisitor.MethodDefinition(node: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected MethodDefinition(node: TSESTree.MethodDefinition): void {
    this.visitMethod(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.visitMethod`
### `ClassVisitor.PrivateIdentifier(): void`

<details><summary>Code</summary>

```ts
protected PrivateIdentifier(): void {
    // intentionally skip
  }
```
</details>

- **Return Type**: `void`
### `ClassVisitor.PropertyDefinition(node: TSESTree.PropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected PropertyDefinition(node: TSESTree.PropertyDefinition): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyDefinition`
### `ClassVisitor.StaticBlock(node: TSESTree.StaticBlock): void`

<details><summary>Code</summary>

```ts
protected StaticBlock(node: TSESTree.StaticBlock): void {
    this.#referencer.scopeManager.nestClassStaticBlockScope(node);

    node.body.forEach(b => this.visit(b));

    this.#referencer.close(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.StaticBlock`
- **Return Type**: `void`
- **Calls**:
  - `this.#referencer.scopeManager.nestClassStaticBlockScope`
  - `node.body.forEach`
  - `this.visit`
  - `this.#referencer.close`
### `ClassVisitor.TSAbstractAccessorProperty(node: TSESTree.TSAbstractAccessorProperty): void`

<details><summary>Code</summary>

```ts
protected TSAbstractAccessorProperty(
    node: TSESTree.TSAbstractAccessorProperty,
  ): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAbstractAccessorProperty`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyDefinition`
### `ClassVisitor.TSAbstractMethodDefinition(node: TSESTree.TSAbstractMethodDefinition): void`

<details><summary>Code</summary>

```ts
protected TSAbstractMethodDefinition(
    node: TSESTree.TSAbstractMethodDefinition,
  ): void {
    this.visitPropertyBase(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAbstractMethodDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyBase`
### `ClassVisitor.TSAbstractPropertyDefinition(node: TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected TSAbstractPropertyDefinition(
    node: TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSAbstractPropertyDefinition`
- **Return Type**: `void`
- **Calls**:
  - `this.visitPropertyDefinition`
### `ClassVisitor.TSIndexSignature(node: TSESTree.TSIndexSignature): void`

<details><summary>Code</summary>

```ts
protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    this.visitType(node);
  }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSIndexSignature`
- **Return Type**: `void`
- **Calls**:
  - `this.visitType`
### `getLiteralMethodKeyName(node: TSESTree.MethodDefinition): number | string | null`

<details><summary>Code</summary>

```ts
function getLiteralMethodKeyName(
  node: TSESTree.MethodDefinition,
): number | string | null {
  if (node.computed && node.key.type === AST_NODE_TYPES.Literal) {
    if (
      typeof node.key.value === 'string' ||
      typeof node.key.value === 'number'
    ) {
      return node.key.value;
    }
  } else if (!node.computed && node.key.type === AST_NODE_TYPES.Identifier) {
    return node.key.name;
  }
  return null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Only if key is one of [identifier, string, number], ts will combine metadata of accessors .
 * class A {
 *   get a() {}
 *   set ['a'](v: Type) {}
 *
 *   get [1]() {}
 *   set [1](v: Type) {}
 *
 *   // Following won't be combined
 *   get [key]() {}
 *   set [key](v: Type) {}
 *
 *   get [true]() {}
 *   set [true](v: Type) {}
 *
 *   get ['a'+'b']() {}
 *   set ['a'+'b']() {}
 * }
 */
```

- **Parameters**:
  - `node: TSESTree.MethodDefinition`
- **Return Type**: `number | string | null`

---

## Classes

### `ClassVisitor`

<details><summary>Class Code</summary>

```ts
export class ClassVisitor extends Visitor {
  readonly #classNode: TSESTree.ClassDeclaration | TSESTree.ClassExpression;
  readonly #referencer: Referencer;

  constructor(
    referencer: Referencer,
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ) {
    super(referencer);
    this.#referencer = referencer;
    this.#classNode = node;
  }

  static visit(
    referencer: Referencer,
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    const classVisitor = new ClassVisitor(referencer, node);
    classVisitor.visitClass(node);
  }

  override visit(node: TSESTree.Node | null | undefined): void {
    // make sure we only handle the nodes we are designed to handle
    if (node && node.type in this) {
      super.visit(node);
    } else {
      this.#referencer.visit(node);
    }
  }

  ///////////////////
  // Visit helpers //
  ///////////////////

  protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    if (node.type === AST_NODE_TYPES.ClassDeclaration && node.id) {
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    node.decorators.forEach(d => this.#referencer.visit(d));

    this.#referencer.scopeManager.nestClassScope(node);

    if (node.id) {
      // define the class name again inside the new scope
      // references to the class should not resolve directly to the parent class
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    this.#referencer.visit(node.superClass);

    // visit the type param declarations
    this.visitType(node.typeParameters);
    // then the usages
    this.visitType(node.superTypeArguments);
    node.implements.forEach(imp => this.visitType(imp));

    this.visit(node.body);

    this.#referencer.close(node);
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
    }
  }

  protected visitMethod(node: TSESTree.MethodDefinition): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value.type === AST_NODE_TYPES.FunctionExpression) {
      this.visitMethodFunction(node.value, node);
    } else {
      this.#referencer.visit(node.value);
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }

  protected visitMethodFunction(
    node: TSESTree.FunctionExpression,
    methodNode: TSESTree.MethodDefinition,
  ): void {
    if (node.id) {
      // FunctionExpression with name creates its special scope;
      // FunctionExpressionNameScope.
      this.#referencer.scopeManager.nestFunctionExpressionNameScope(node);
    }

    node.params.forEach(param => {
      param.decorators.forEach(d => this.visit(d));
    });

    // Consider this function is in the MethodDefinition.
    this.#referencer.scopeManager.nestFunctionScope(node, true);

    /**
     * class A {
     *   @meta     // <--- check this
     *   foo(a: Type) {}
     *
     *   @meta     // <--- check this
     *   foo(): Type {}
     * }
     */
    let withMethodDecorators = !!methodNode.decorators.length;
    /**
     * class A {
     *   foo(
     *     @meta    // <--- check this
     *     a: Type
     *   ) {}
     *
     *   set foo(
     *     @meta    // <--- EXCEPT this. TS do nothing for this
     *     a: Type
     *   ) {}
     * }
     */
    withMethodDecorators ||=
      methodNode.kind !== 'set' &&
      node.params.some(param => param.decorators.length);
    if (!withMethodDecorators && methodNode.kind === 'set') {
      const keyName = getLiteralMethodKeyName(methodNode);

      /**
       * class A {
       *   @meta      // <--- check this
       *   get a() {}
       *   set ['a'](v: Type) {}
       * }
       */
      if (
        keyName != null &&
        this.#classNode.body.body.find(
          (node): node is TSESTree.MethodDefinition =>
            node !== methodNode &&
            node.type === AST_NODE_TYPES.MethodDefinition &&
            // Node must both be static or not
            node.static === methodNode.static &&
            getLiteralMethodKeyName(node) === keyName,
        )?.decorators.length
      ) {
        withMethodDecorators = true;
      }
    }

    /**
     * @meta      // <--- check this
     * class A {
     *   constructor(a: Type) {}
     * }
     */
    if (
      !withMethodDecorators &&
      methodNode.kind === 'constructor' &&
      this.#classNode.decorators.length
    ) {
      withMethodDecorators = true;
    }

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.#referencer
            .currentScope()
            .defineIdentifier(
              pattern,
              new ParameterDefinition(pattern, node, info.rest),
            );

          this.#referencer.referencingDefaultValue(
            pattern,
            info.assignments,
            null,
            true,
          );
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    this.#referencer.visitChildren(node.body);
    this.#referencer.close(node);
  }

  protected visitPropertyBase(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value) {
      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.scopeManager.nestClassFieldInitializerScope(
          node.value,
        );
      }

      this.#referencer.visit(node.value);

      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.close(node.value);
      }
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }

  protected visitPropertyDefinition(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyBase(node);
    /**
     * class A {
     *   @meta     // <--- check this
     *   foo: Type;
     * }
     */
    this.visitType(node.typeAnnotation);
  }

  protected visitType(node: TSESTree.Node | null | undefined): void {
    if (!node) {
      return;
    }
    TypeVisitor.visit(this.#referencer, node);
  }

  /////////////////////
  // Visit selectors //
  /////////////////////

  protected AccessorProperty(node: TSESTree.AccessorProperty): void {
    this.visitPropertyDefinition(node);
  }

  protected ClassBody(node: TSESTree.ClassBody): void {
    // this is here on purpose so that this visitor explicitly declares visitors
    // for all nodes it cares about (see the instance visit method above)
    this.visitChildren(node);
  }

  protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.visit(node);
  }

  protected MethodDefinition(node: TSESTree.MethodDefinition): void {
    this.visitMethod(node);
  }

  protected PrivateIdentifier(): void {
    // intentionally skip
  }

  protected PropertyDefinition(node: TSESTree.PropertyDefinition): void {
    this.visitPropertyDefinition(node);
  }

  protected StaticBlock(node: TSESTree.StaticBlock): void {
    this.#referencer.scopeManager.nestClassStaticBlockScope(node);

    node.body.forEach(b => this.visit(b));

    this.#referencer.close(node);
  }

  protected TSAbstractAccessorProperty(
    node: TSESTree.TSAbstractAccessorProperty,
  ): void {
    this.visitPropertyDefinition(node);
  }

  protected TSAbstractMethodDefinition(
    node: TSESTree.TSAbstractMethodDefinition,
  ): void {
    this.visitPropertyBase(node);
  }

  protected TSAbstractPropertyDefinition(
    node: TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyDefinition(node);
  }

  protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    this.visitType(node);
  }
}
```
</details>

#### Methods

##### `visit(referencer: Referencer, node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
static visit(
    referencer: Referencer,
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    const classVisitor = new ClassVisitor(referencer, node);
    classVisitor.visitClass(node);
  }
```
</details>

##### `visit(node: TSESTree.Node | null | undefined): void`

<details><summary>Code</summary>

```ts
override visit(node: TSESTree.Node | null | undefined): void {
    // make sure we only handle the nodes we are designed to handle
    if (node && node.type in this) {
      super.visit(node);
    } else {
      this.#referencer.visit(node);
    }
  }
```
</details>

##### `visitClass(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression): void`

<details><summary>Code</summary>

```ts
protected visitClass(
    node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  ): void {
    if (node.type === AST_NODE_TYPES.ClassDeclaration && node.id) {
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    node.decorators.forEach(d => this.#referencer.visit(d));

    this.#referencer.scopeManager.nestClassScope(node);

    if (node.id) {
      // define the class name again inside the new scope
      // references to the class should not resolve directly to the parent class
      this.#referencer
        .currentScope()
        .defineIdentifier(node.id, new ClassNameDefinition(node.id, node));
    }

    this.#referencer.visit(node.superClass);

    // visit the type param declarations
    this.visitType(node.typeParameters);
    // then the usages
    this.visitType(node.superTypeArguments);
    node.implements.forEach(imp => this.visitType(imp));

    this.visit(node.body);

    this.#referencer.close(node);
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
    }
  }
```
</details>

##### `visitMethod(node: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected visitMethod(node: TSESTree.MethodDefinition): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value.type === AST_NODE_TYPES.FunctionExpression) {
      this.visitMethodFunction(node.value, node);
    } else {
      this.#referencer.visit(node.value);
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }
```
</details>

##### `visitMethodFunction(node: TSESTree.FunctionExpression, methodNode: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected visitMethodFunction(
    node: TSESTree.FunctionExpression,
    methodNode: TSESTree.MethodDefinition,
  ): void {
    if (node.id) {
      // FunctionExpression with name creates its special scope;
      // FunctionExpressionNameScope.
      this.#referencer.scopeManager.nestFunctionExpressionNameScope(node);
    }

    node.params.forEach(param => {
      param.decorators.forEach(d => this.visit(d));
    });

    // Consider this function is in the MethodDefinition.
    this.#referencer.scopeManager.nestFunctionScope(node, true);

    /**
     * class A {
     *   @meta     // <--- check this
     *   foo(a: Type) {}
     *
     *   @meta     // <--- check this
     *   foo(): Type {}
     * }
     */
    let withMethodDecorators = !!methodNode.decorators.length;
    /**
     * class A {
     *   foo(
     *     @meta    // <--- check this
     *     a: Type
     *   ) {}
     *
     *   set foo(
     *     @meta    // <--- EXCEPT this. TS do nothing for this
     *     a: Type
     *   ) {}
     * }
     */
    withMethodDecorators ||=
      methodNode.kind !== 'set' &&
      node.params.some(param => param.decorators.length);
    if (!withMethodDecorators && methodNode.kind === 'set') {
      const keyName = getLiteralMethodKeyName(methodNode);

      /**
       * class A {
       *   @meta      // <--- check this
       *   get a() {}
       *   set ['a'](v: Type) {}
       * }
       */
      if (
        keyName != null &&
        this.#classNode.body.body.find(
          (node): node is TSESTree.MethodDefinition =>
            node !== methodNode &&
            node.type === AST_NODE_TYPES.MethodDefinition &&
            // Node must both be static or not
            node.static === methodNode.static &&
            getLiteralMethodKeyName(node) === keyName,
        )?.decorators.length
      ) {
        withMethodDecorators = true;
      }
    }

    /**
     * @meta      // <--- check this
     * class A {
     *   constructor(a: Type) {}
     * }
     */
    if (
      !withMethodDecorators &&
      methodNode.kind === 'constructor' &&
      this.#classNode.decorators.length
    ) {
      withMethodDecorators = true;
    }

    // Process parameter declarations.
    for (const param of node.params) {
      this.visitPattern(
        param,
        (pattern, info) => {
          this.#referencer
            .currentScope()
            .defineIdentifier(
              pattern,
              new ParameterDefinition(pattern, node, info.rest),
            );

          this.#referencer.referencingDefaultValue(
            pattern,
            info.assignments,
            null,
            true,
          );
        },
        { processRightHandNodes: true },
      );
      this.visitFunctionParameterTypeAnnotation(param);
    }

    this.visitType(node.returnType);
    this.visitType(node.typeParameters);

    this.#referencer.visitChildren(node.body);
    this.#referencer.close(node);
  }
```
</details>

##### `visitPropertyBase(node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected visitPropertyBase(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractMethodDefinition
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    if (node.computed) {
      this.#referencer.visit(node.key);
    }

    if (node.value) {
      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.scopeManager.nestClassFieldInitializerScope(
          node.value,
        );
      }

      this.#referencer.visit(node.value);

      if (
        node.type === AST_NODE_TYPES.PropertyDefinition ||
        node.type === AST_NODE_TYPES.AccessorProperty
      ) {
        this.#referencer.close(node.value);
      }
    }

    node.decorators.forEach(d => this.#referencer.visit(d));
  }
```
</details>

##### `visitPropertyDefinition(node: | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected visitPropertyDefinition(
    node:
      | TSESTree.AccessorProperty
      | TSESTree.PropertyDefinition
      | TSESTree.TSAbstractAccessorProperty
      | TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyBase(node);
    /**
     * class A {
     *   @meta     // <--- check this
     *   foo: Type;
     * }
     */
    this.visitType(node.typeAnnotation);
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
    TypeVisitor.visit(this.#referencer, node);
  }
```
</details>

##### `AccessorProperty(node: TSESTree.AccessorProperty): void`

<details><summary>Code</summary>

```ts
protected AccessorProperty(node: TSESTree.AccessorProperty): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

##### `ClassBody(node: TSESTree.ClassBody): void`

<details><summary>Code</summary>

```ts
protected ClassBody(node: TSESTree.ClassBody): void {
    // this is here on purpose so that this visitor explicitly declares visitors
    // for all nodes it cares about (see the instance visit method above)
    this.visitChildren(node);
  }
```
</details>

##### `Identifier(node: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
protected Identifier(node: TSESTree.Identifier): void {
    this.#referencer.visit(node);
  }
```
</details>

##### `MethodDefinition(node: TSESTree.MethodDefinition): void`

<details><summary>Code</summary>

```ts
protected MethodDefinition(node: TSESTree.MethodDefinition): void {
    this.visitMethod(node);
  }
```
</details>

##### `PrivateIdentifier(): void`

<details><summary>Code</summary>

```ts
protected PrivateIdentifier(): void {
    // intentionally skip
  }
```
</details>

##### `PropertyDefinition(node: TSESTree.PropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected PropertyDefinition(node: TSESTree.PropertyDefinition): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

##### `StaticBlock(node: TSESTree.StaticBlock): void`

<details><summary>Code</summary>

```ts
protected StaticBlock(node: TSESTree.StaticBlock): void {
    this.#referencer.scopeManager.nestClassStaticBlockScope(node);

    node.body.forEach(b => this.visit(b));

    this.#referencer.close(node);
  }
```
</details>

##### `TSAbstractAccessorProperty(node: TSESTree.TSAbstractAccessorProperty): void`

<details><summary>Code</summary>

```ts
protected TSAbstractAccessorProperty(
    node: TSESTree.TSAbstractAccessorProperty,
  ): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

##### `TSAbstractMethodDefinition(node: TSESTree.TSAbstractMethodDefinition): void`

<details><summary>Code</summary>

```ts
protected TSAbstractMethodDefinition(
    node: TSESTree.TSAbstractMethodDefinition,
  ): void {
    this.visitPropertyBase(node);
  }
```
</details>

##### `TSAbstractPropertyDefinition(node: TSESTree.TSAbstractPropertyDefinition): void`

<details><summary>Code</summary>

```ts
protected TSAbstractPropertyDefinition(
    node: TSESTree.TSAbstractPropertyDefinition,
  ): void {
    this.visitPropertyDefinition(node);
  }
```
</details>

##### `TSIndexSignature(node: TSESTree.TSIndexSignature): void`

<details><summary>Code</summary>

```ts
protected TSIndexSignature(node: TSESTree.TSIndexSignature): void {
    this.visitType(node);
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