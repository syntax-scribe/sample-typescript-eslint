[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-arguments.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 15 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 2 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-type-arguments.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `findFirstResult` | `../util` |
| `getParserServices` | `../util` |
| `isTypeReferenceType` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `i` | `number` | const | `esParameters.params.length - 1` | ✗ |
| `arg` | `any` | const | `esParameters.params[i]` | ✗ |


---

## Functions

### `getTypeForComparison(type: ts.Type): {
      type: ts.Type;
      typeArguments: readonly ts.Type[];
    }`

<details><summary>Code</summary>

```ts
function getTypeForComparison(type: ts.Type): {
      type: ts.Type;
      typeArguments: readonly ts.Type[];
    } {
      if (isTypeReferenceType(type)) {
        return {
          type: type.target,
          typeArguments: checker.getTypeArguments(type),
        };
      }
      return {
        type,
        typeArguments: [],
      };
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `{
      type: ts.Type;
      typeArguments: readonly ts.Type[];
    }`
- **Calls**:
  - `isTypeReferenceType (from ../util)`
  - `checker.getTypeArguments`
### `checkTSArgsAndParameters(esParameters: TSESTree.TSTypeParameterInstantiation, typeParameters: readonly ts.TypeParameterDeclaration[]): void`

<details><summary>Code</summary>

```ts
function checkTSArgsAndParameters(
      esParameters: TSESTree.TSTypeParameterInstantiation,
      typeParameters: readonly ts.TypeParameterDeclaration[],
    ): void {
      // Just check the last one. Must specify previous type parameters if the last one is specified.
      const i = esParameters.params.length - 1;
      const arg = esParameters.params[i];
      const param = typeParameters.at(i);
      if (!param?.default) {
        return;
      }

      // TODO: would like checker.areTypesEquivalent. https://github.com/Microsoft/TypeScript/issues/13502
      const defaultType = checker.getTypeAtLocation(param.default);
      const argType = services.getTypeAtLocation(arg);
      // this check should handle some of the most simple cases of like strings, numbers, etc
      if (defaultType !== argType) {
        // For more complex types (like aliases to generic object types) - TS won't always create a
        // global shared type object for the type - so we need to resort to manually comparing the
        // reference type and the passed type arguments.
        // Also - in case there are aliases - we need to resolve them before we do checks
        const defaultTypeResolved = getTypeForComparison(defaultType);
        const argTypeResolved = getTypeForComparison(argType);
        if (
          // ensure the resolved type AND all the parameters are the same
          defaultTypeResolved.type !== argTypeResolved.type ||
          defaultTypeResolved.typeArguments.length !==
            argTypeResolved.typeArguments.length ||
          defaultTypeResolved.typeArguments.some(
            (t, i) => t !== argTypeResolved.typeArguments[i],
          )
        ) {
          return;
        }
      }

      context.report({
        node: arg,
        messageId: 'unnecessaryTypeParameter',
        fix: fixer =>
          fixer.removeRange(
            i === 0
              ? esParameters.range
              : [esParameters.params[i - 1].range[1], arg.range[1]],
          ),
      });
    }
```
</details>

- **Parameters**:
  - `esParameters: TSESTree.TSTypeParameterInstantiation`
  - `typeParameters: readonly ts.TypeParameterDeclaration[]`
- **Return Type**: `void`
- **Calls**:
  - `typeParameters.at`
  - `checker.getTypeAtLocation`
  - `services.getTypeAtLocation`
  - `getTypeForComparison`
  - `defaultTypeResolved.typeArguments.some`
  - `context.report`
  - `fixer.removeRange`
- **Internal Comments**:
```
// Just check the last one. Must specify previous type parameters if the last one is specified. (x2)
// TODO: would like checker.areTypesEquivalent. https://github.com/Microsoft/TypeScript/issues/13502 (x2)
// this check should handle some of the most simple cases of like strings, numbers, etc
// For more complex types (like aliases to generic object types) - TS won't always create a (x2)
// global shared type object for the type - so we need to resort to manually comparing the (x2)
// reference type and the passed type arguments. (x2)
// Also - in case there are aliases - we need to resolve them before we do checks (x2)
// ensure the resolved type AND all the parameters are the same (x5)
```

### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.removeRange(
            i === 0
              ? esParameters.range
              : [esParameters.params[i - 1].range[1], arg.range[1]],
          )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.removeRange(
            i === 0
              ? esParameters.range
              : [esParameters.params[i - 1].range[1], arg.range[1]],
          )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.removeRange(
            i === 0
              ? esParameters.range
              : [esParameters.params[i - 1].range[1], arg.range[1]],
          )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `fix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer =>
          fixer.removeRange(
            i === 0
              ? esParameters.range
              : [esParameters.params[i - 1].range[1], arg.range[1]],
          )
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `fixer.removeRange`
### `getTypeParametersFromNode(node: TSESTree.TSTypeParameterInstantiation, tsNode: ParameterCapableTSNode, checker: ts.TypeChecker): readonly ts.TypeParameterDeclaration[] | undefined`

<details><summary>Code</summary>

```ts
function getTypeParametersFromNode(
  node: TSESTree.TSTypeParameterInstantiation,
  tsNode: ParameterCapableTSNode,
  checker: ts.TypeChecker,
): readonly ts.TypeParameterDeclaration[] | undefined {
  if (ts.isExpressionWithTypeArguments(tsNode)) {
    return getTypeParametersFromType(node, tsNode.expression, checker);
  }

  if (ts.isTypeReferenceNode(tsNode)) {
    return getTypeParametersFromType(node, tsNode.typeName, checker);
  }

  if (
    ts.isCallExpression(tsNode) ||
    ts.isNewExpression(tsNode) ||
    ts.isTaggedTemplateExpression(tsNode) ||
    ts.isJsxOpeningElement(tsNode) ||
    ts.isJsxSelfClosingElement(tsNode)
  ) {
    return getTypeParametersFromCall(node, tsNode, checker);
  }

  return undefined;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameterInstantiation`
  - `tsNode: ParameterCapableTSNode`
  - `checker: ts.TypeChecker`
- **Return Type**: `readonly ts.TypeParameterDeclaration[] | undefined`
- **Calls**:
  - `ts.isExpressionWithTypeArguments`
  - `getTypeParametersFromType`
  - `ts.isTypeReferenceNode`
  - `ts.isCallExpression`
  - `ts.isNewExpression`
  - `ts.isTaggedTemplateExpression`
  - `ts.isJsxOpeningElement`
  - `ts.isJsxSelfClosingElement`
  - `getTypeParametersFromCall`
### `getTypeParametersFromType(node: TSESTree.TSTypeParameterInstantiation, type: ts.ClassDeclaration | ts.EntityName | ts.Expression, checker: ts.TypeChecker): readonly ts.TypeParameterDeclaration[] | undefined`

<details><summary>Code</summary>

```ts
function getTypeParametersFromType(
  node: TSESTree.TSTypeParameterInstantiation,
  type: ts.ClassDeclaration | ts.EntityName | ts.Expression,
  checker: ts.TypeChecker,
): readonly ts.TypeParameterDeclaration[] | undefined {
  const symAtLocation = checker.getSymbolAtLocation(type);
  if (!symAtLocation) {
    return undefined;
  }

  const sym = getAliasedSymbol(symAtLocation, checker);
  const declarations = sym.getDeclarations();

  if (!declarations) {
    return undefined;
  }

  const sortedDeclaraions = sortDeclarationsByTypeValueContext(
    node,
    declarations,
  );
  return findFirstResult(sortedDeclaraions, decl => {
    if (
      ts.isTypeAliasDeclaration(decl) ||
      ts.isInterfaceDeclaration(decl) ||
      ts.isClassLike(decl)
    ) {
      return decl.typeParameters;
    }
    if (ts.isVariableDeclaration(decl)) {
      return getConstructSignatureDeclaration(symAtLocation, checker)
        ?.typeParameters;
    }
    return undefined;
  });
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameterInstantiation`
  - `type: ts.ClassDeclaration | ts.EntityName | ts.Expression`
  - `checker: ts.TypeChecker`
- **Return Type**: `readonly ts.TypeParameterDeclaration[] | undefined`
- **Calls**:
  - `checker.getSymbolAtLocation`
  - `getAliasedSymbol`
  - `sym.getDeclarations`
  - `sortDeclarationsByTypeValueContext`
  - `findFirstResult (from ../util)`
  - `ts.isTypeAliasDeclaration`
  - `ts.isInterfaceDeclaration`
  - `ts.isClassLike`
  - `ts.isVariableDeclaration`
  - `getConstructSignatureDeclaration`
### `getTypeParametersFromCall(node: TSESTree.TSTypeParameterInstantiation, tsNode: | ts.CallExpression
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement
    | ts.NewExpression
    | ts.TaggedTemplateExpression, checker: ts.TypeChecker): readonly ts.TypeParameterDeclaration[] | undefined`

<details><summary>Code</summary>

```ts
function getTypeParametersFromCall(
  node: TSESTree.TSTypeParameterInstantiation,
  tsNode:
    | ts.CallExpression
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement
    | ts.NewExpression
    | ts.TaggedTemplateExpression,
  checker: ts.TypeChecker,
): readonly ts.TypeParameterDeclaration[] | undefined {
  const sig = checker.getResolvedSignature(tsNode);
  const sigDecl = sig?.getDeclaration();
  if (!sigDecl) {
    return ts.isNewExpression(tsNode)
      ? getTypeParametersFromType(node, tsNode.expression, checker)
      : undefined;
  }

  return sigDecl.typeParameters;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameterInstantiation`
  - `tsNode: | ts.CallExpression
    | ts.JsxOpeningElement
    | ts.JsxSelfClosingElement
    | ts.NewExpression
    | ts.TaggedTemplateExpression`
  - `checker: ts.TypeChecker`
- **Return Type**: `readonly ts.TypeParameterDeclaration[] | undefined`
- **Calls**:
  - `checker.getResolvedSignature`
  - `sig?.getDeclaration`
  - `ts.isNewExpression`
  - `getTypeParametersFromType`
### `getAliasedSymbol(symbol: ts.Symbol, checker: ts.TypeChecker): ts.Symbol`

<details><summary>Code</summary>

```ts
function getAliasedSymbol(
  symbol: ts.Symbol,
  checker: ts.TypeChecker,
): ts.Symbol {
  return tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.Alias)
    ? checker.getAliasedSymbol(symbol)
    : symbol;
}
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
  - `checker: ts.TypeChecker`
- **Return Type**: `ts.Symbol`
- **Calls**:
  - `tsutils.isSymbolFlagSet`
  - `checker.getAliasedSymbol`
### `isInTypeContext(node: TSESTree.TSTypeParameterInstantiation): boolean`

<details><summary>Code</summary>

```ts
function isInTypeContext(node: TSESTree.TSTypeParameterInstantiation) {
  return (
    node.parent.type === AST_NODE_TYPES.TSInterfaceHeritage ||
    node.parent.type === AST_NODE_TYPES.TSTypeReference ||
    node.parent.type === AST_NODE_TYPES.TSClassImplements
  );
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameterInstantiation`
- **Return Type**: `boolean`
### `isTypeContextDeclaration(decl: ts.Declaration): any`

<details><summary>Code</summary>

```ts
function isTypeContextDeclaration(decl: ts.Declaration) {
  return ts.isTypeAliasDeclaration(decl) || ts.isInterfaceDeclaration(decl);
}
```
</details>

- **Parameters**:
  - `decl: ts.Declaration`
- **Return Type**: `any`
- **Calls**:
  - `ts.isTypeAliasDeclaration`
  - `ts.isInterfaceDeclaration`
### `typeFirstCompare(declA: ts.Declaration, declB: ts.Declaration): number`

<details><summary>Code</summary>

```ts
function typeFirstCompare(declA: ts.Declaration, declB: ts.Declaration) {
  const aIsType = isTypeContextDeclaration(declA);
  const bIsType = isTypeContextDeclaration(declB);

  return Number(bIsType) - Number(aIsType);
}
```
</details>

- **Parameters**:
  - `declA: ts.Declaration`
  - `declB: ts.Declaration`
- **Return Type**: `number`
- **Calls**:
  - `isTypeContextDeclaration`
  - `Number`
### `sortDeclarationsByTypeValueContext(node: TSESTree.TSTypeParameterInstantiation, declarations: ts.Declaration[]): ts.Declaration[]`

<details><summary>Code</summary>

```ts
function sortDeclarationsByTypeValueContext(
  node: TSESTree.TSTypeParameterInstantiation,
  declarations: ts.Declaration[],
) {
  const sorted = [...declarations].sort(typeFirstCompare);
  if (isInTypeContext(node)) {
    return sorted;
  }
  return sorted.reverse();
}
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameterInstantiation`
  - `declarations: ts.Declaration[]`
- **Return Type**: `ts.Declaration[]`
- **Calls**:
  - `[...declarations].sort`
  - `isInTypeContext`
  - `sorted.reverse`
### `getConstructSignatureDeclaration(symbol: ts.Symbol, checker: ts.TypeChecker): ts.SignatureDeclaration | undefined`

<details><summary>Code</summary>

```ts
function getConstructSignatureDeclaration(
  symbol: ts.Symbol,
  checker: ts.TypeChecker,
): ts.SignatureDeclaration | undefined {
  const type = checker.getTypeOfSymbol(symbol);
  const sig = type.getConstructSignatures();
  return sig.at(0)?.getDeclaration();
}
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
  - `checker: ts.TypeChecker`
- **Return Type**: `ts.SignatureDeclaration | undefined`
- **Calls**:
  - `checker.getTypeOfSymbol`
  - `type.getConstructSignatures`
  - `sig.at(0)?.getDeclaration`

---

## Type Aliases

### `ParameterCapableTSNode`

```ts
type ParameterCapableTSNode = | ts.CallExpression
  | ts.ExpressionWithTypeArguments
  | ts.ImportTypeNode
  | ts.JsxOpeningElement
  | ts.JsxSelfClosingElement
  | ts.NewExpression
  | ts.TaggedTemplateExpression
  | ts.TypeQueryNode
  | ts.TypeReferenceNode;
```

### `MessageIds`

```ts
type MessageIds = 'unnecessaryTypeParameter';
```


---