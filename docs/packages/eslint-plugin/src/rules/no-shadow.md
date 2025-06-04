[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-shadow.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 23 |
| 📦 Imports | 9 |
| 📊 Variables & Constants | 29 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-shadow.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `ScopeType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isDefinitionFile` | `../util` |
| `isTypeImport` | `../util/isTypeImport` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `allowedFunctionVariableDefTypes` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.TSCallSignatureDeclaration,
  AST_NODE_TYPES.TSFunctionType,
  AST_NODE_TYPES.TSMethodSignature,
  AST_NODE_TYPES.TSEmptyBodyFunctionExpression,
  AST_NODE_TYPES.TSDeclareFunction,
  AST_NODE_TYPES.TSConstructSignatureDeclaration,
  AST_NODE_TYPES.TSConstructorType,
])` | ✗ |
| `functionsHoistedNodes` | `Set<any>` | const | `new Set([AST_NODE_TYPES.FunctionDeclaration])` | ✗ |
| `typesHoistedNodes` | `Set<any>` | const | `new Set([
  AST_NODE_TYPES.TSInterfaceDeclaration,
  AST_NODE_TYPES.TSTypeAliasDeclaration,
])` | ✗ |
| `isShadowedValue` | `any` | const | `!('isValueVariable' in shadowed) ||
        !firstDefinition ||
        (!isTypeImport(firstDefinition) && shadowed.isValueVariable)` | ✗ |
| `isShadowedValue` | `any` | const | `'isValueVariable' in shadowed ? shadowed.isValueVariable : true` | ✗ |
| `typeParameter` | `any` | const | `variable.identifiers[0].parent` | ✗ |
| `typeParameterDecl` | `any` | const | `typeParameter.parent` | ✗ |
| `functionExpr` | `any` | const | `typeParameterDecl.parent` | ✗ |
| `methodDefinition` | `any` | const | `functionExpr.parent` | ✗ |
| `typeParameter` | `any` | const | `variable.identifiers[0].parent` | ✗ |
| `typeParameterDecl` | `any` | const | `typeParameter.parent` | ✗ |
| `classDecl` | `any` | const | `typeParameterDecl.parent` | ✗ |
| `block` | `any` | const | `variable.scope.block` | ✗ |
| `block` | `any` | const | `variable.scope.block` | ✗ |
| `currentNode` | `any` | let/var | `node` | ✗ |
| `upper` | `any` | const | `scope.upper` | ✗ |
| `fun` | `any` | const | `variableScope.block` | ✗ |
| `node` | `any` | let/var | `outerDef.name as TSESTree.Node | undefined` | ✗ |
| `location` | `any` | const | `callExpression.range[1]` | ✗ |
| `outerScope` | `any` | const | `scopeVar.scope` | ✗ |
| `outer` | `any` | const | `outerDef?.parent?.range` | ✗ |
| `innerScope` | `any` | const | `variable.scope` | ✗ |
| `inner` | `any` | const | `innerDef?.name.range` | ✗ |
| `fileName` | `any` | const | `context.filename` | ✗ |
| `variables` | `any` | const | `scope.variables` | ✗ |
| `shadowed` | `any` | const | `scope.upper
          ? ASTUtils.findVariable(scope.upper, variable.name)
          : null` | ✗ |
| `isESLintGlobal` | `boolean` | const | `'writeable' in shadowed` | ✗ |
| `stack` | `any[]` | const | `[...globalScope.childScopes]` | ✗ |
| `scope` | `any` | const | `stack.pop()!` | ✗ |


---

## Functions

### `isGlobalAugmentation(scope: TSESLint.Scope.Scope): boolean`

<details><summary>Code</summary>

```ts
function isGlobalAugmentation(scope: TSESLint.Scope.Scope): boolean {
      return (
        (scope.type === ScopeType.tsModule && scope.block.kind === 'global') ||
        (!!scope.upper && isGlobalAugmentation(scope.upper))
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if a scope is a TypeScript module augmenting the global namespace.
     */
```

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
- **Return Type**: `boolean`
- **Calls**:
  - `isGlobalAugmentation`
### `isThisParam(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isThisParam(variable: TSESLint.Scope.Variable): boolean {
      return (
        variable.defs[0].type === DefinitionType.Parameter &&
        variable.name === 'this'
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if variable is a `this` parameter.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
### `isTypeValueShadow(variable: TSESLint.Scope.Variable, shadowed: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isTypeValueShadow(
      variable: TSESLint.Scope.Variable,
      shadowed: TSESLint.Scope.Variable,
    ): boolean {
      if (options.ignoreTypeValueShadow !== true) {
        return false;
      }

      if (!('isValueVariable' in variable)) {
        // this shouldn't happen...
        return false;
      }

      const firstDefinition = shadowed.defs.at(0);
      const isShadowedValue =
        !('isValueVariable' in shadowed) ||
        !firstDefinition ||
        (!isTypeImport(firstDefinition) && shadowed.isValueVariable);
      return variable.isValueVariable !== isShadowedValue;
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `shadowed: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `shadowed.defs.at`
  - `isTypeImport (from ../util/isTypeImport)`
- **Internal Comments**:
```
// this shouldn't happen...
```

### `isFunctionTypeParameterNameValueShadow(variable: TSESLint.Scope.Variable, shadowed: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isFunctionTypeParameterNameValueShadow(
      variable: TSESLint.Scope.Variable,
      shadowed: TSESLint.Scope.Variable,
    ): boolean {
      if (options.ignoreFunctionTypeParameterNameValueShadow !== true) {
        return false;
      }

      if (!('isValueVariable' in variable)) {
        // this shouldn't happen...
        return false;
      }

      const isShadowedValue =
        'isValueVariable' in shadowed ? shadowed.isValueVariable : true;
      if (!isShadowedValue) {
        return false;
      }

      return variable.defs.every(def =>
        allowedFunctionVariableDefTypes.has(def.node.type),
      );
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `shadowed: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `variable.defs.every`
  - `allowedFunctionVariableDefTypes.has`
- **Internal Comments**:
```
// this shouldn't happen...
```

### `isGenericOfStaticMethod(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isGenericOfStaticMethod(
      variable: TSESLint.Scope.Variable,
    ): boolean {
      if (!('isTypeVariable' in variable)) {
        // this shouldn't happen...
        return false;
      }

      if (!variable.isTypeVariable) {
        return false;
      }

      if (variable.identifiers.length === 0) {
        return false;
      }

      const typeParameter = variable.identifiers[0].parent;
      if (typeParameter.type !== AST_NODE_TYPES.TSTypeParameter) {
        return false;
      }
      const typeParameterDecl = typeParameter.parent;
      if (
        typeParameterDecl.type !== AST_NODE_TYPES.TSTypeParameterDeclaration
      ) {
        return false;
      }
      const functionExpr = typeParameterDecl.parent;
      if (
        functionExpr.type !== AST_NODE_TYPES.FunctionExpression &&
        functionExpr.type !== AST_NODE_TYPES.TSEmptyBodyFunctionExpression
      ) {
        return false;
      }
      const methodDefinition = functionExpr.parent;
      if (methodDefinition.type !== AST_NODE_TYPES.MethodDefinition) {
        return false;
      }
      return methodDefinition.static;
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// this shouldn't happen...
```

### `isGenericOfClass(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isGenericOfClass(variable: TSESLint.Scope.Variable): boolean {
      if (!('isTypeVariable' in variable)) {
        // this shouldn't happen...
        return false;
      }

      if (!variable.isTypeVariable) {
        return false;
      }

      if (variable.identifiers.length === 0) {
        return false;
      }

      const typeParameter = variable.identifiers[0].parent;
      if (typeParameter.type !== AST_NODE_TYPES.TSTypeParameter) {
        return false;
      }
      const typeParameterDecl = typeParameter.parent;
      if (
        typeParameterDecl.type !== AST_NODE_TYPES.TSTypeParameterDeclaration
      ) {
        return false;
      }
      const classDecl = typeParameterDecl.parent;
      return (
        classDecl.type === AST_NODE_TYPES.ClassDeclaration ||
        classDecl.type === AST_NODE_TYPES.ClassExpression
      );
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// this shouldn't happen...
```

### `isGenericOfAStaticMethodShadow(variable: TSESLint.Scope.Variable, shadowed: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isGenericOfAStaticMethodShadow(
      variable: TSESLint.Scope.Variable,
      shadowed: TSESLint.Scope.Variable,
    ): boolean {
      return isGenericOfStaticMethod(variable) && isGenericOfClass(shadowed);
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `shadowed: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `isGenericOfStaticMethod`
  - `isGenericOfClass`
### `isImportDeclaration(definition: | TSESTree.ImportDeclaration
        | TSESTree.TSImportEqualsDeclaration): definition is TSESTree.ImportDeclaration`

<details><summary>Code</summary>

```ts
function isImportDeclaration(
      definition:
        | TSESTree.ImportDeclaration
        | TSESTree.TSImportEqualsDeclaration,
    ): definition is TSESTree.ImportDeclaration {
      return definition.type === AST_NODE_TYPES.ImportDeclaration;
    }
```
</details>

- **Parameters**:
  - `definition: | TSESTree.ImportDeclaration
        | TSESTree.TSImportEqualsDeclaration`
- **Return Type**: `definition is TSESTree.ImportDeclaration`
### `isExternalModuleDeclarationWithName(scope: TSESLint.Scope.Scope, name: string): boolean`

<details><summary>Code</summary>

```ts
function isExternalModuleDeclarationWithName(
      scope: TSESLint.Scope.Scope,
      name: string,
    ): boolean {
      return (
        scope.type === ScopeType.tsModule &&
        scope.block.id.type === AST_NODE_TYPES.Literal &&
        scope.block.id.value === name
      );
    }
```
</details>

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
  - `name: string`
- **Return Type**: `boolean`
### `isExternalDeclarationMerging(scope: TSESLint.Scope.Scope, variable: TSESLint.Scope.Variable, shadowed: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isExternalDeclarationMerging(
      scope: TSESLint.Scope.Scope,
      variable: TSESLint.Scope.Variable,
      shadowed: TSESLint.Scope.Variable,
    ): boolean {
      const [firstDefinition] = shadowed.defs;
      const [secondDefinition] = variable.defs;

      return (
        isTypeImport(firstDefinition) &&
        isImportDeclaration(firstDefinition.parent) &&
        isExternalModuleDeclarationWithName(
          scope,
          firstDefinition.parent.source.value,
        ) &&
        (secondDefinition.node.type === AST_NODE_TYPES.TSInterfaceDeclaration ||
          secondDefinition.node.type === AST_NODE_TYPES.TSTypeAliasDeclaration)
      );
    }
```
</details>

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
  - `variable: TSESLint.Scope.Variable`
  - `shadowed: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeImport (from ../util/isTypeImport)`
  - `isImportDeclaration`
  - `isExternalModuleDeclarationWithName`
### `isAllowed(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isAllowed(variable: TSESLint.Scope.Variable): boolean {
      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      return options.allow!.includes(variable.name);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Check if variable name is allowed.
     * @param variable The variable to check.
     * @returns Whether or not the variable name is allowed.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `options.allow!.includes`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion
```

### `isDuplicatedClassNameVariable(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isDuplicatedClassNameVariable(
      variable: TSESLint.Scope.Variable,
    ): boolean {
      const block = variable.scope.block;

      return (
        block.type === AST_NODE_TYPES.ClassDeclaration &&
        block.id === variable.identifiers[0]
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a variable of the class name in the class scope of ClassDeclaration.
     *
     * ClassDeclaration creates two variables of its name into its outer scope and its class scope.
     * So we should ignore the variable in the class scope.
     * @param variable The variable to check.
     * @returns Whether or not the variable of the class name in the class scope of ClassDeclaration.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
### `isDuplicatedEnumNameVariable(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isDuplicatedEnumNameVariable(
      variable: TSESLint.Scope.Variable,
    ): boolean {
      const block = variable.scope.block;

      return (
        block.type === AST_NODE_TYPES.TSEnumDeclaration &&
        block.id === variable.identifiers[0]
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a variable of the class name in the class scope of TSEnumDeclaration.
     *
     * TSEnumDeclaration creates two variables of its name into its outer scope and its class scope.
     * So we should ignore the variable in the class scope.
     * @param variable The variable to check.
     * @returns Whether or not the variable of the class name in the class scope of TSEnumDeclaration.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
### `isInRange(node: TSESTree.Node | null, location: number): boolean | null`

<details><summary>Code</summary>

```ts
function isInRange(
      node: TSESTree.Node | null,
      location: number,
    ): boolean | null {
      return node && node.range[0] <= location && location <= node.range[1];
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks whether or not a given location is inside of the range of a given node.
     * @param node An node to check.
     * @param location A location to check.
     * @returns `true` if the location is inside of the range of the node.
     */
```

- **Parameters**:
  - `node: TSESTree.Node | null`
  - `location: number`
- **Return Type**: `boolean | null`
### `findSelfOrAncestor(node: TSESTree.Node | undefined, match: (node: TSESTree.Node) => boolean): TSESTree.Node | undefined`

<details><summary>Code</summary>

```ts
function findSelfOrAncestor(
      node: TSESTree.Node | undefined,
      match: (node: TSESTree.Node) => boolean,
    ): TSESTree.Node | undefined {
      let currentNode = node;

      while (currentNode && !match(currentNode)) {
        currentNode = currentNode.parent;
      }
      return currentNode;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Searches from the current node through its ancestry to find a matching node.
     * @param node a node to get.
     * @param match a callback that checks whether or not the node verifies its condition or not.
     * @returns the matching node.
     */
```

- **Parameters**:
  - `node: TSESTree.Node | undefined`
  - `match: (node: TSESTree.Node) => boolean`
- **Return Type**: `TSESTree.Node | undefined`
- **Calls**:
  - `match`
### `getOuterScope(scope: TSESLint.Scope.Scope): TSESLint.Scope.Scope | null`

<details><summary>Code</summary>

```ts
function getOuterScope(
      scope: TSESLint.Scope.Scope,
    ): TSESLint.Scope.Scope | null {
      const upper = scope.upper;

      if (upper?.type === ScopeType.functionExpressionName) {
        return upper.upper;
      }
      return upper;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Finds function's outer scope.
     * @param scope Function's own scope.
     * @returns Function's outer scope.
     */
```

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
- **Return Type**: `TSESLint.Scope.Scope | null`
### `isInitPatternNode(variable: TSESLint.Scope.Variable, shadowedVariable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isInitPatternNode(
      variable: TSESLint.Scope.Variable,
      shadowedVariable: TSESLint.Scope.Variable,
    ): boolean {
      const outerDef = shadowedVariable.defs.at(0);

      if (!outerDef) {
        return false;
      }

      const { variableScope } = variable.scope;

      if (
        !(
          (variableScope.block.type ===
            AST_NODE_TYPES.ArrowFunctionExpression ||
            variableScope.block.type === AST_NODE_TYPES.FunctionExpression) &&
          getOuterScope(variableScope) === shadowedVariable.scope
        )
      ) {
        return false;
      }

      const fun = variableScope.block;
      const { parent } = fun;

      const callExpression = findSelfOrAncestor(
        parent,
        node => node.type === AST_NODE_TYPES.CallExpression,
      );

      if (!callExpression) {
        return false;
      }

      let node = outerDef.name as TSESTree.Node | undefined;
      const location = callExpression.range[1];

      while (node) {
        if (node.type === AST_NODE_TYPES.VariableDeclarator) {
          if (isInRange(node.init, location)) {
            return true;
          }
          if (
            (node.parent.parent.type === AST_NODE_TYPES.ForInStatement ||
              node.parent.parent.type === AST_NODE_TYPES.ForOfStatement) &&
            isInRange(node.parent.parent.right, location)
          ) {
            return true;
          }
          break;
        } else if (node.type === AST_NODE_TYPES.AssignmentPattern) {
          if (isInRange(node.right, location)) {
            return true;
          }
        } else if (
          [
            AST_NODE_TYPES.ArrowFunctionExpression,
            AST_NODE_TYPES.CatchClause,
            AST_NODE_TYPES.ClassDeclaration,
            AST_NODE_TYPES.ClassExpression,
            AST_NODE_TYPES.ExportNamedDeclaration,
            AST_NODE_TYPES.FunctionDeclaration,
            AST_NODE_TYPES.FunctionExpression,
            AST_NODE_TYPES.ImportDeclaration,
          ].includes(node.type)
        ) {
          break;
        }

        node = node.parent;
      }

      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a variable and a shadowedVariable have the same init pattern ancestor.
     * @param variable a variable to check.
     * @param shadowedVariable a shadowedVariable to check.
     * @returns Whether or not the variable and the shadowedVariable have the same init pattern ancestor.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `shadowedVariable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `shadowedVariable.defs.at`
  - `getOuterScope`
  - `findSelfOrAncestor`
  - `isInRange`
  - `[
            AST_NODE_TYPES.ArrowFunctionExpression,
            AST_NODE_TYPES.CatchClause,
            AST_NODE_TYPES.ClassDeclaration,
            AST_NODE_TYPES.ClassExpression,
            AST_NODE_TYPES.ExportNamedDeclaration,
            AST_NODE_TYPES.FunctionDeclaration,
            AST_NODE_TYPES.FunctionExpression,
            AST_NODE_TYPES.ImportDeclaration,
          ].includes`
### `isOnInitializer(variable: TSESLint.Scope.Variable, scopeVar: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isOnInitializer(
      variable: TSESLint.Scope.Variable,
      scopeVar: TSESLint.Scope.Variable,
    ): boolean {
      const outerScope = scopeVar.scope;
      const outerDef = scopeVar.defs.at(0);
      const outer = outerDef?.parent?.range;
      const innerScope = variable.scope;
      const innerDef = variable.defs.at(0);
      const inner = innerDef?.name.range;

      return !!(
        outer &&
        inner &&
        outer[0] < inner[0] &&
        inner[1] < outer[1] &&
        ((innerDef.type === DefinitionType.FunctionName &&
          innerDef.node.type === AST_NODE_TYPES.FunctionExpression) ||
          innerDef.node.type === AST_NODE_TYPES.ClassExpression) &&
        outerScope === innerScope.upper
      );
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a variable is inside the initializer of scopeVar.
     *
     * To avoid reporting at declarations such as `var a = function a() {};`.
     * But it should report `var a = function(a) {};` or `var a = function() { function a() {} };`.
     * @param variable The variable to check.
     * @param scopeVar The scope variable to look for.
     * @returns Whether or not the variable is inside initializer of scopeVar.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `scopeVar: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `scopeVar.defs.at`
  - `variable.defs.at`
### `getNameRange(variable: TSESLint.Scope.Variable): TSESTree.Range | undefined`

<details><summary>Code</summary>

```ts
function getNameRange(
      variable: TSESLint.Scope.Variable,
    ): TSESTree.Range | undefined {
      const def = variable.defs.at(0);
      return def?.name.range;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Get a range of a variable's identifier node.
     * @param variable The variable to get.
     * @returns The range of the variable's identifier node.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `TSESTree.Range | undefined`
- **Calls**:
  - `variable.defs.at`
### `isInTdz(variable: TSESLint.Scope.Variable, scopeVar: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isInTdz(
      variable: TSESLint.Scope.Variable,
      scopeVar: TSESLint.Scope.Variable,
    ): boolean {
      const outerDef = scopeVar.defs.at(0);
      const inner = getNameRange(variable);
      const outer = getNameRange(scopeVar);

      if (!inner || !outer || inner[1] >= outer[0]) {
        return false;
      }

      if (!outerDef) {
        return true;
      }

      if (options.hoist === 'functions') {
        return !functionsHoistedNodes.has(outerDef.node.type);
      }

      if (options.hoist === 'types') {
        return !typesHoistedNodes.has(outerDef.node.type);
      }

      if (options.hoist === 'functions-and-types') {
        return (
          !functionsHoistedNodes.has(outerDef.node.type) &&
          !typesHoistedNodes.has(outerDef.node.type)
        );
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if a variable is in TDZ of scopeVar.
     * @param variable The variable to check.
     * @param scopeVar The variable of TDZ.
     * @returns Whether or not the variable is in TDZ of scopeVar.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `scopeVar: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `scopeVar.defs.at`
  - `getNameRange`
  - `functionsHoistedNodes.has`
  - `typesHoistedNodes.has`
### `getDeclaredLocation(variable: TSESLint.Scope.Variable): { column: number; global: false; line: number } | { global: true }`

<details><summary>Code</summary>

```ts
function getDeclaredLocation(
      variable: TSESLint.Scope.Variable,
    ): { column: number; global: false; line: number } | { global: true } {
      const identifier = variable.identifiers.at(0);
      if (identifier) {
        return {
          column: identifier.loc.start.column + 1,
          global: false,
          line: identifier.loc.start.line,
        };
      }
      return {
        global: true,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Get declared line and column of a variable.
     * @param  variable The variable to get.
     * @returns The declared line and column of the variable.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `{ column: number; global: false; line: number } | { global: true }`
- **Calls**:
  - `variable.identifiers.at`
### `isDeclareInDTSFile(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isDeclareInDTSFile(variable: TSESLint.Scope.Variable): boolean {
      const fileName = context.filename;
      if (!isDefinitionFile(fileName)) {
        return false;
      }
      return variable.defs.some(def => {
        return (
          (def.type === DefinitionType.Variable && def.parent.declare) ||
          (def.type === DefinitionType.ClassName && def.node.declare) ||
          (def.type === DefinitionType.TSEnumName && def.node.declare) ||
          (def.type === DefinitionType.TSModuleName && def.node.declare)
        );
      });
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks if the initialization of a variable has the declare modifier in a
     * definition file.
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
- **Calls**:
  - `isDefinitionFile (from ../util)`
  - `variable.defs.some`
### `checkForShadows(scope: TSESLint.Scope.Scope): void`

<details><summary>Code</summary>

```ts
function checkForShadows(scope: TSESLint.Scope.Scope): void {
      // ignore global augmentation
      if (isGlobalAugmentation(scope)) {
        return;
      }

      const variables = scope.variables;

      for (const variable of variables) {
        // ignore "arguments"
        if (variable.identifiers.length === 0) {
          continue;
        }

        // this params are pseudo-params that cannot be shadowed
        if (isThisParam(variable)) {
          continue;
        }

        // ignore variables of a class name in the class scope of ClassDeclaration
        if (isDuplicatedClassNameVariable(variable)) {
          continue;
        }

        // ignore variables of a class name in the class scope of ClassDeclaration
        if (isDuplicatedEnumNameVariable(variable)) {
          continue;
        }

        // ignore configured allowed names
        if (isAllowed(variable)) {
          continue;
        }

        // ignore variables with the declare keyword in .d.ts files
        if (isDeclareInDTSFile(variable)) {
          continue;
        }

        // Gets shadowed variable.
        const shadowed = scope.upper
          ? ASTUtils.findVariable(scope.upper, variable.name)
          : null;
        if (!shadowed) {
          continue;
        }

        // ignore type value variable shadowing if configured
        if (isTypeValueShadow(variable, shadowed)) {
          continue;
        }

        // ignore function type parameter name shadowing if configured
        if (isFunctionTypeParameterNameValueShadow(variable, shadowed)) {
          continue;
        }

        // ignore static class method generic shadowing class generic
        // this is impossible for the scope analyser to understand
        // so we have to handle this manually in this rule
        if (isGenericOfAStaticMethodShadow(variable, shadowed)) {
          continue;
        }

        if (isExternalDeclarationMerging(scope, variable, shadowed)) {
          continue;
        }

        const isESLintGlobal = 'writeable' in shadowed;
        if (
          (shadowed.identifiers.length > 0 ||
            (options.builtinGlobals && isESLintGlobal)) &&
          !isOnInitializer(variable, shadowed) &&
          !(
            options.ignoreOnInitialization &&
            isInitPatternNode(variable, shadowed)
          ) &&
          !(options.hoist !== 'all' && isInTdz(variable, shadowed))
        ) {
          const location = getDeclaredLocation(shadowed);

          context.report({
            node: variable.identifiers[0],
            ...(location.global
              ? {
                  messageId: 'noShadowGlobal',
                  data: {
                    name: variable.name,
                  },
                }
              : {
                  messageId: 'noShadow',
                  data: {
                    name: variable.name,
                    shadowedColumn: location.column,
                    shadowedLine: location.line,
                  },
                }),
          });
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Checks the current context for shadowed variables.
     * @param scope Fixme
     */
```

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
- **Return Type**: `void`
- **Calls**:
  - `isGlobalAugmentation`
  - `isThisParam`
  - `isDuplicatedClassNameVariable`
  - `isDuplicatedEnumNameVariable`
  - `isAllowed`
  - `isDeclareInDTSFile`
  - `ASTUtils.findVariable`
  - `isTypeValueShadow`
  - `isFunctionTypeParameterNameValueShadow`
  - `isGenericOfAStaticMethodShadow`
  - `isExternalDeclarationMerging`
  - `isOnInitializer`
  - `isInitPatternNode`
  - `isInTdz`
  - `getDeclaredLocation`
  - `context.report`
- **Internal Comments**:
```
// ignore global augmentation
// ignore "arguments"
// this params are pseudo-params that cannot be shadowed
// ignore variables of a class name in the class scope of ClassDeclaration (x2)
// ignore configured allowed names
// ignore variables with the declare keyword in .d.ts files
// Gets shadowed variable. (x2)
// ignore type value variable shadowing if configured
// ignore function type parameter name shadowing if configured
// ignore static class method generic shadowing class generic
// this is impossible for the scope analyser to understand
// so we have to handle this manually in this rule
```


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'noShadow' | 'noShadowGlobal';
```

### `Options`

```ts
type Options = [
  {
    allow?: string[];
    builtinGlobals?: boolean;
    hoist?: 'all' | 'functions' | 'functions-and-types' | 'never' | 'types';
    ignoreFunctionTypeParameterNameValueShadow?: boolean;
    ignoreOnInitialization?: boolean;
    ignoreTypeValueShadow?: boolean;
  },
];
```


---