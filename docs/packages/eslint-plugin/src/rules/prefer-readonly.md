[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `prefer-readonly.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Classes](#classes)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 16
- **Classes**: 1
- **Imports**: 9
- **Interfaces**: 0
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/prefer-readonly.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `nullThrows` | `../util` |
| `typeIsOrHasBaseType` | `../util` |
| `getMemberHeadLoc` | `../util/getMemberHeadLoc` |
| `getParameterPropertyHeadLoc` | `../util/getMemberHeadLoc` |


---

## Functions

### `handlePropertyAccessExpression(node: ts.PropertyAccessExpression, parent: ts.Node, classScope: ClassScope): void`

<details><summary>Code</summary>

```ts
function handlePropertyAccessExpression(
      node: ts.PropertyAccessExpression,
      parent: ts.Node,
      classScope: ClassScope,
    ): void {
      if (ts.isBinaryExpression(parent)) {
        handleParentBinaryExpression(node, parent, classScope);
        return;
      }

      if (ts.isDeleteExpression(parent) || isDestructuringAssignment(node)) {
        classScope.addVariableModification(node);
        return;
      }

      if (
        ts.isPostfixUnaryExpression(parent) ||
        ts.isPrefixUnaryExpression(parent)
      ) {
        handleParentPostfixOrPrefixUnaryExpression(parent, classScope);
      }
    }
```
</details>

- **Parameters**:
  - `node: ts.PropertyAccessExpression`
  - `parent: ts.Node`
  - `classScope: ClassScope`
- **Return Type**: `void`
- **Calls**:
  - `ts.isBinaryExpression`
  - `handleParentBinaryExpression`
  - `ts.isDeleteExpression`
  - `isDestructuringAssignment`
  - `classScope.addVariableModification`
  - `ts.isPostfixUnaryExpression`
  - `ts.isPrefixUnaryExpression`
  - `handleParentPostfixOrPrefixUnaryExpression`
### `handleParentBinaryExpression(node: ts.PropertyAccessExpression, parent: ts.BinaryExpression, classScope: ClassScope): void`

<details><summary>Code</summary>

```ts
function handleParentBinaryExpression(
      node: ts.PropertyAccessExpression,
      parent: ts.BinaryExpression,
      classScope: ClassScope,
    ): void {
      if (
        parent.left === node &&
        tsutils.isAssignmentKind(parent.operatorToken.kind)
      ) {
        classScope.addVariableModification(node);
      }
    }
```
</details>

- **Parameters**:
  - `node: ts.PropertyAccessExpression`
  - `parent: ts.BinaryExpression`
  - `classScope: ClassScope`
- **Return Type**: `void`
- **Calls**:
  - `tsutils.isAssignmentKind`
  - `classScope.addVariableModification`
### `handleParentPostfixOrPrefixUnaryExpression(node: ts.PostfixUnaryExpression | ts.PrefixUnaryExpression, classScope: ClassScope): void`

<details><summary>Code</summary>

```ts
function handleParentPostfixOrPrefixUnaryExpression(
      node: ts.PostfixUnaryExpression | ts.PrefixUnaryExpression,
      classScope: ClassScope,
    ): void {
      if (
        node.operator === ts.SyntaxKind.PlusPlusToken ||
        node.operator === ts.SyntaxKind.MinusMinusToken
      ) {
        classScope.addVariableModification(
          node.operand as ts.PropertyAccessExpression,
        );
      }
    }
```
</details>

- **Parameters**:
  - `node: ts.PostfixUnaryExpression | ts.PrefixUnaryExpression`
  - `classScope: ClassScope`
- **Return Type**: `void`
- **Calls**:
  - `classScope.addVariableModification`
### `isDestructuringAssignment(node: ts.PropertyAccessExpression): boolean`

<details><summary>Code</summary>

```ts
function isDestructuringAssignment(
      node: ts.PropertyAccessExpression,
    ): boolean {
      let current = node.parent as ts.Node | undefined;

      while (current) {
        const parent = current.parent;

        if (
          ts.isObjectLiteralExpression(parent) ||
          ts.isArrayLiteralExpression(parent) ||
          ts.isSpreadAssignment(parent) ||
          (ts.isSpreadElement(parent) &&
            ts.isArrayLiteralExpression(parent.parent))
        ) {
          current = parent;
        } else if (
          ts.isBinaryExpression(parent) &&
          !ts.isPropertyAccessExpression(current)
        ) {
          return (
            parent.left === current &&
            parent.operatorToken.kind === ts.SyntaxKind.EqualsToken
          );
        } else {
          break;
        }
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `node: ts.PropertyAccessExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `ts.isObjectLiteralExpression`
  - `ts.isArrayLiteralExpression`
  - `ts.isSpreadAssignment`
  - `ts.isSpreadElement`
  - `ts.isBinaryExpression`
  - `ts.isPropertyAccessExpression`
### `isFunctionScopeBoundaryInStack(node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression
        | TSESTree.MethodDefinition): boolean`

<details><summary>Code</summary>

```ts
function isFunctionScopeBoundaryInStack(
      node:
        | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression
        | TSESTree.MethodDefinition,
    ): boolean {
      if (classScopeStack.length === 0) {
        return false;
      }

      const tsNode = services.esTreeNodeToTSNodeMap.get(node);
      if (ts.isConstructorDeclaration(tsNode)) {
        return false;
      }

      return tsutils.isFunctionScopeBoundary(tsNode);
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
        | TSESTree.FunctionDeclaration
        | TSESTree.FunctionExpression
        | TSESTree.MethodDefinition`
- **Return Type**: `boolean`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `ts.isConstructorDeclaration`
  - `tsutils.isFunctionScopeBoundary`
### `getEsNodesFromViolatingNode(violatingNode: ParameterOrPropertyDeclaration): { esNode: TSESTree.Node; nameNode: TSESTree.Node }`

<details><summary>Code</summary>

```ts
function getEsNodesFromViolatingNode(
      violatingNode: ParameterOrPropertyDeclaration,
    ): { esNode: TSESTree.Node; nameNode: TSESTree.Node } {
      return {
        esNode: services.tsNodeToESTreeNodeMap.get(violatingNode),
        nameNode: services.tsNodeToESTreeNodeMap.get(violatingNode.name),
      };
    }
```
</details>

- **Parameters**:
  - `violatingNode: ParameterOrPropertyDeclaration`
- **Return Type**: `{ esNode: TSESTree.Node; nameNode: TSESTree.Node }`
- **Calls**:
  - `services.tsNodeToESTreeNodeMap.get`
### `getTypeAnnotationForViolatingNode(node: TSESTree.Node, type: ts.Type, initializerType: ts.Type): any`

<details><summary>Code</summary>

```ts
function getTypeAnnotationForViolatingNode(
      node: TSESTree.Node,
      type: ts.Type,
      initializerType: ts.Type,
    ) {
      const annotation = checker.typeToString(type);

      // verify the about-to-be-added type annotation is in-scope
      if (tsutils.isTypeFlagSet(initializerType, ts.TypeFlags.EnumLiteral)) {
        const scope = context.sourceCode.getScope(node);
        const variable = ASTUtils.findVariable(scope, annotation);

        if (variable == null) {
          return null;
        }

        const definition = variable.defs.find(def => def.isTypeDefinition);

        if (definition == null) {
          return null;
        }

        const definitionType = services.getTypeAtLocation(definition.node);

        if (definitionType !== type) {
          return null;
        }
      }

      return annotation;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `type: ts.Type`
  - `initializerType: ts.Type`
- **Return Type**: `any`
- **Calls**:
  - `checker.typeToString`
  - `tsutils.isTypeFlagSet`
  - `context.sourceCode.getScope`
  - `ASTUtils.findVariable`
  - `variable.defs.find`
  - `services.getTypeAtLocation`
- **Internal Comments**:
```
// verify the about-to-be-added type annotation is in-scope
```

### `ClassScope.addDeclaredVariable(node: ParameterOrPropertyDeclaration): void`

<details><summary>Code</summary>

```ts
public addDeclaredVariable(node: ParameterOrPropertyDeclaration): void {
    if (
      !(
        tsutils.isModifierFlagSet(node, ts.ModifierFlags.Private) ||
        node.name.kind === ts.SyntaxKind.PrivateIdentifier
      ) ||
      tsutils.isModifierFlagSet(
        node,
        ts.ModifierFlags.Accessor | ts.ModifierFlags.Readonly,
      ) ||
      ts.isComputedPropertyName(node.name)
    ) {
      return;
    }

    if (
      this.onlyInlineLambdas &&
      node.initializer != null &&
      !ts.isArrowFunction(node.initializer)
    ) {
      return;
    }

    (tsutils.isModifierFlagSet(node, ts.ModifierFlags.Static)
      ? this.privateModifiableStatics
      : this.privateModifiableMembers
    ).set(node.name.getText(), node);
  }
```
</details>

- **Parameters**:
  - `node: ParameterOrPropertyDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `tsutils.isModifierFlagSet`
  - `ts.isComputedPropertyName`
  - `ts.isArrowFunction`
  - `(tsutils.isModifierFlagSet(node, ts.ModifierFlags.Static)
      ? this.privateModifiableStatics
      : this.privateModifiableMembers
    ).set`
  - `node.name.getText`
### `ClassScope.addVariableModification(node: ts.PropertyAccessExpression): void`

<details><summary>Code</summary>

```ts
public addVariableModification(node: ts.PropertyAccessExpression): void {
    const modifierType = this.checker.getTypeAtLocation(node.expression);

    const relationOfModifierTypeToClass =
      this.getTypeToClassRelation(modifierType);

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance &&
      this.constructorScopeDepth === DIRECTLY_INSIDE_CONSTRUCTOR
    ) {
      this.memberVariableWithConstructorModifications.add(node.name.text);
      return;
    }

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.memberVariableModifications.add(node.name.text);
    }
    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Class ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.staticVariableModifications.add(node.name.text);
    }
  }
```
</details>

- **Parameters**:
  - `node: ts.PropertyAccessExpression`
- **Return Type**: `void`
- **Calls**:
  - `this.checker.getTypeAtLocation`
  - `this.getTypeToClassRelation`
  - `this.memberVariableWithConstructorModifications.add`
  - `this.memberVariableModifications.add`
  - `this.staticVariableModifications.add`
### `ClassScope.enterConstructor(node: | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration): void`

<details><summary>Code</summary>

```ts
public enterConstructor(
    node:
      | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration,
  ): void {
    this.constructorScopeDepth = DIRECTLY_INSIDE_CONSTRUCTOR;

    for (const parameter of node.parameters) {
      if (tsutils.isModifierFlagSet(parameter, ts.ModifierFlags.Private)) {
        this.addDeclaredVariable(parameter);
      }
    }
  }
```
</details>

- **Parameters**:
  - `node: | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `tsutils.isModifierFlagSet`
  - `this.addDeclaredVariable`
### `ClassScope.enterNonConstructor(): void`

<details><summary>Code</summary>

```ts
public enterNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth += 1;
    }
  }
```
</details>

- **Return Type**: `void`
### `ClassScope.exitConstructor(): void`

<details><summary>Code</summary>

```ts
public exitConstructor(): void {
    this.constructorScopeDepth = OUTSIDE_CONSTRUCTOR;
  }
```
</details>

- **Return Type**: `void`
### `ClassScope.exitNonConstructor(): void`

<details><summary>Code</summary>

```ts
public exitNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth -= 1;
    }
  }
```
</details>

- **Return Type**: `void`
### `ClassScope.finalizeUnmodifiedPrivateNonReadonlys(): ParameterOrPropertyDeclaration[]`

<details><summary>Code</summary>

```ts
public finalizeUnmodifiedPrivateNonReadonlys(): ParameterOrPropertyDeclaration[] {
    this.memberVariableModifications.forEach(variableName => {
      this.privateModifiableMembers.delete(variableName);
    });

    this.staticVariableModifications.forEach(variableName => {
      this.privateModifiableStatics.delete(variableName);
    });

    return [
      ...this.privateModifiableMembers.values(),
      ...this.privateModifiableStatics.values(),
    ];
  }
```
</details>

- **Return Type**: `ParameterOrPropertyDeclaration[]`
- **Calls**:
  - `this.memberVariableModifications.forEach`
  - `this.privateModifiableMembers.delete`
  - `this.staticVariableModifications.forEach`
  - `this.privateModifiableStatics.delete`
  - `this.privateModifiableMembers.values`
  - `this.privateModifiableStatics.values`
### `ClassScope.getTypeToClassRelation(type: ts.Type): TypeToClassRelation`

<details><summary>Code</summary>

```ts
public getTypeToClassRelation(type: ts.Type): TypeToClassRelation {
    if (type.isIntersection()) {
      let result: TypeToClassRelation = TypeToClassRelation.None;
      for (const subType of type.types) {
        const subTypeResult = this.getTypeToClassRelation(subType);
        switch (subTypeResult) {
          case TypeToClassRelation.Class:
            if (result === TypeToClassRelation.Instance) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Class;
            break;
          case TypeToClassRelation.Instance:
            if (result === TypeToClassRelation.Class) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Instance;
            break;
        }
      }
      return result;
    }
    if (type.isUnion()) {
      // any union of class/instance and something else will prevent access to
      // private members, so we assume that union consists only of classes
      // or class instances, because otherwise tsc will report an error
      return this.getTypeToClassRelation(type.types[0]);
    }

    if (!type.getSymbol() || !typeIsOrHasBaseType(type, this.classType)) {
      return TypeToClassRelation.None;
    }

    const typeIsClass =
      tsutils.isObjectType(type) &&
      tsutils.isObjectFlagSet(type, ts.ObjectFlags.Anonymous);

    if (typeIsClass) {
      return TypeToClassRelation.Class;
    }

    return TypeToClassRelation.Instance;
  }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `TypeToClassRelation`
- **Calls**:
  - `type.isIntersection`
  - `this.getTypeToClassRelation`
  - `type.isUnion`
  - `type.getSymbol`
  - `typeIsOrHasBaseType (from ../util)`
  - `tsutils.isObjectType`
  - `tsutils.isObjectFlagSet`
- **Internal Comments**:
```
// any union of class/instance and something else will prevent access to
// private members, so we assume that union consists only of classes
// or class instances, because otherwise tsc will report an error
```

### `ClassScope.memberHasConstructorModifications(name: string): boolean`

<details><summary>Code</summary>

```ts
public memberHasConstructorModifications(name: string) {
    return this.memberVariableWithConstructorModifications.has(name);
  }
```
</details>

- **Parameters**:
  - `name: string`
- **Return Type**: `boolean`
- **Calls**:
  - `this.memberVariableWithConstructorModifications.has`

---

## Classes

### `ClassScope`

<details><summary>Class Code</summary>

```ts
class ClassScope {
  private readonly classType: ts.Type;
  private constructorScopeDepth = OUTSIDE_CONSTRUCTOR;
  private readonly memberVariableModifications = new Set<string>();
  private readonly memberVariableWithConstructorModifications =
    new Set<string>();
  private readonly privateModifiableMembers = new Map<
    string,
    ParameterOrPropertyDeclaration
  >();

  private readonly privateModifiableStatics = new Map<
    string,
    ParameterOrPropertyDeclaration
  >();

  private readonly staticVariableModifications = new Set<string>();

  public constructor(
    private readonly checker: ts.TypeChecker,
    classNode: ts.ClassLikeDeclaration,
    private readonly onlyInlineLambdas?: boolean,
  ) {
    const classType = checker.getTypeAtLocation(classNode);
    if (tsutils.isIntersectionType(classType)) {
      this.classType = classType.types[0];
    } else {
      this.classType = classType;
    }

    for (const member of classNode.members) {
      if (ts.isPropertyDeclaration(member)) {
        this.addDeclaredVariable(member);
      }
    }
  }

  public addDeclaredVariable(node: ParameterOrPropertyDeclaration): void {
    if (
      !(
        tsutils.isModifierFlagSet(node, ts.ModifierFlags.Private) ||
        node.name.kind === ts.SyntaxKind.PrivateIdentifier
      ) ||
      tsutils.isModifierFlagSet(
        node,
        ts.ModifierFlags.Accessor | ts.ModifierFlags.Readonly,
      ) ||
      ts.isComputedPropertyName(node.name)
    ) {
      return;
    }

    if (
      this.onlyInlineLambdas &&
      node.initializer != null &&
      !ts.isArrowFunction(node.initializer)
    ) {
      return;
    }

    (tsutils.isModifierFlagSet(node, ts.ModifierFlags.Static)
      ? this.privateModifiableStatics
      : this.privateModifiableMembers
    ).set(node.name.getText(), node);
  }

  public addVariableModification(node: ts.PropertyAccessExpression): void {
    const modifierType = this.checker.getTypeAtLocation(node.expression);

    const relationOfModifierTypeToClass =
      this.getTypeToClassRelation(modifierType);

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance &&
      this.constructorScopeDepth === DIRECTLY_INSIDE_CONSTRUCTOR
    ) {
      this.memberVariableWithConstructorModifications.add(node.name.text);
      return;
    }

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.memberVariableModifications.add(node.name.text);
    }
    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Class ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.staticVariableModifications.add(node.name.text);
    }
  }

  public enterConstructor(
    node:
      | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration,
  ): void {
    this.constructorScopeDepth = DIRECTLY_INSIDE_CONSTRUCTOR;

    for (const parameter of node.parameters) {
      if (tsutils.isModifierFlagSet(parameter, ts.ModifierFlags.Private)) {
        this.addDeclaredVariable(parameter);
      }
    }
  }

  public enterNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth += 1;
    }
  }

  public exitConstructor(): void {
    this.constructorScopeDepth = OUTSIDE_CONSTRUCTOR;
  }

  public exitNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth -= 1;
    }
  }

  public finalizeUnmodifiedPrivateNonReadonlys(): ParameterOrPropertyDeclaration[] {
    this.memberVariableModifications.forEach(variableName => {
      this.privateModifiableMembers.delete(variableName);
    });

    this.staticVariableModifications.forEach(variableName => {
      this.privateModifiableStatics.delete(variableName);
    });

    return [
      ...this.privateModifiableMembers.values(),
      ...this.privateModifiableStatics.values(),
    ];
  }

  public getTypeToClassRelation(type: ts.Type): TypeToClassRelation {
    if (type.isIntersection()) {
      let result: TypeToClassRelation = TypeToClassRelation.None;
      for (const subType of type.types) {
        const subTypeResult = this.getTypeToClassRelation(subType);
        switch (subTypeResult) {
          case TypeToClassRelation.Class:
            if (result === TypeToClassRelation.Instance) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Class;
            break;
          case TypeToClassRelation.Instance:
            if (result === TypeToClassRelation.Class) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Instance;
            break;
        }
      }
      return result;
    }
    if (type.isUnion()) {
      // any union of class/instance and something else will prevent access to
      // private members, so we assume that union consists only of classes
      // or class instances, because otherwise tsc will report an error
      return this.getTypeToClassRelation(type.types[0]);
    }

    if (!type.getSymbol() || !typeIsOrHasBaseType(type, this.classType)) {
      return TypeToClassRelation.None;
    }

    const typeIsClass =
      tsutils.isObjectType(type) &&
      tsutils.isObjectFlagSet(type, ts.ObjectFlags.Anonymous);

    if (typeIsClass) {
      return TypeToClassRelation.Class;
    }

    return TypeToClassRelation.Instance;
  }

  public memberHasConstructorModifications(name: string) {
    return this.memberVariableWithConstructorModifications.has(name);
  }
}
```
</details>

#### Methods

##### `addDeclaredVariable(node: ParameterOrPropertyDeclaration): void`

<details><summary>Code</summary>

```ts
public addDeclaredVariable(node: ParameterOrPropertyDeclaration): void {
    if (
      !(
        tsutils.isModifierFlagSet(node, ts.ModifierFlags.Private) ||
        node.name.kind === ts.SyntaxKind.PrivateIdentifier
      ) ||
      tsutils.isModifierFlagSet(
        node,
        ts.ModifierFlags.Accessor | ts.ModifierFlags.Readonly,
      ) ||
      ts.isComputedPropertyName(node.name)
    ) {
      return;
    }

    if (
      this.onlyInlineLambdas &&
      node.initializer != null &&
      !ts.isArrowFunction(node.initializer)
    ) {
      return;
    }

    (tsutils.isModifierFlagSet(node, ts.ModifierFlags.Static)
      ? this.privateModifiableStatics
      : this.privateModifiableMembers
    ).set(node.name.getText(), node);
  }
```
</details>

##### `addVariableModification(node: ts.PropertyAccessExpression): void`

<details><summary>Code</summary>

```ts
public addVariableModification(node: ts.PropertyAccessExpression): void {
    const modifierType = this.checker.getTypeAtLocation(node.expression);

    const relationOfModifierTypeToClass =
      this.getTypeToClassRelation(modifierType);

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance &&
      this.constructorScopeDepth === DIRECTLY_INSIDE_CONSTRUCTOR
    ) {
      this.memberVariableWithConstructorModifications.add(node.name.text);
      return;
    }

    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Instance ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.memberVariableModifications.add(node.name.text);
    }
    if (
      relationOfModifierTypeToClass === TypeToClassRelation.Class ||
      relationOfModifierTypeToClass === TypeToClassRelation.ClassAndInstance
    ) {
      this.staticVariableModifications.add(node.name.text);
    }
  }
```
</details>

##### `enterConstructor(node: | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration): void`

<details><summary>Code</summary>

```ts
public enterConstructor(
    node:
      | ts.ConstructorDeclaration
      | ts.GetAccessorDeclaration
      | ts.MethodDeclaration
      | ts.SetAccessorDeclaration,
  ): void {
    this.constructorScopeDepth = DIRECTLY_INSIDE_CONSTRUCTOR;

    for (const parameter of node.parameters) {
      if (tsutils.isModifierFlagSet(parameter, ts.ModifierFlags.Private)) {
        this.addDeclaredVariable(parameter);
      }
    }
  }
```
</details>

##### `enterNonConstructor(): void`

<details><summary>Code</summary>

```ts
public enterNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth += 1;
    }
  }
```
</details>

##### `exitConstructor(): void`

<details><summary>Code</summary>

```ts
public exitConstructor(): void {
    this.constructorScopeDepth = OUTSIDE_CONSTRUCTOR;
  }
```
</details>

##### `exitNonConstructor(): void`

<details><summary>Code</summary>

```ts
public exitNonConstructor(): void {
    if (this.constructorScopeDepth !== OUTSIDE_CONSTRUCTOR) {
      this.constructorScopeDepth -= 1;
    }
  }
```
</details>

##### `finalizeUnmodifiedPrivateNonReadonlys(): ParameterOrPropertyDeclaration[]`

<details><summary>Code</summary>

```ts
public finalizeUnmodifiedPrivateNonReadonlys(): ParameterOrPropertyDeclaration[] {
    this.memberVariableModifications.forEach(variableName => {
      this.privateModifiableMembers.delete(variableName);
    });

    this.staticVariableModifications.forEach(variableName => {
      this.privateModifiableStatics.delete(variableName);
    });

    return [
      ...this.privateModifiableMembers.values(),
      ...this.privateModifiableStatics.values(),
    ];
  }
```
</details>

##### `getTypeToClassRelation(type: ts.Type): TypeToClassRelation`

<details><summary>Code</summary>

```ts
public getTypeToClassRelation(type: ts.Type): TypeToClassRelation {
    if (type.isIntersection()) {
      let result: TypeToClassRelation = TypeToClassRelation.None;
      for (const subType of type.types) {
        const subTypeResult = this.getTypeToClassRelation(subType);
        switch (subTypeResult) {
          case TypeToClassRelation.Class:
            if (result === TypeToClassRelation.Instance) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Class;
            break;
          case TypeToClassRelation.Instance:
            if (result === TypeToClassRelation.Class) {
              return TypeToClassRelation.ClassAndInstance;
            }
            result = TypeToClassRelation.Instance;
            break;
        }
      }
      return result;
    }
    if (type.isUnion()) {
      // any union of class/instance and something else will prevent access to
      // private members, so we assume that union consists only of classes
      // or class instances, because otherwise tsc will report an error
      return this.getTypeToClassRelation(type.types[0]);
    }

    if (!type.getSymbol() || !typeIsOrHasBaseType(type, this.classType)) {
      return TypeToClassRelation.None;
    }

    const typeIsClass =
      tsutils.isObjectType(type) &&
      tsutils.isObjectFlagSet(type, ts.ObjectFlags.Anonymous);

    if (typeIsClass) {
      return TypeToClassRelation.Class;
    }

    return TypeToClassRelation.Instance;
  }
```
</details>

##### `memberHasConstructorModifications(name: string): boolean`

<details><summary>Code</summary>

```ts
public memberHasConstructorModifications(name: string) {
    return this.memberVariableWithConstructorModifications.has(name);
  }
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'preferReadonly';
```

### `Options`

```ts
type Options = [
  {
    onlyInlineLambdas?: boolean;
  },
];
```

### `ParameterOrPropertyDeclaration`

```ts
type ParameterOrPropertyDeclaration = | ts.ParameterDeclaration
  | ts.PropertyDeclaration;
```


---