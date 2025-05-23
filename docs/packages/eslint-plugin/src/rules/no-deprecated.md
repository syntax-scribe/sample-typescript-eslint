[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-deprecated.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 12
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 4

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-deprecated.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TypeOrValueSpecifier` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `nullThrows` | `../util` |
| `typeOrValueSpecifiersSchema` | `../util` |
| `typeMatchesSomeSpecifier` | `../util` |


---

## Functions

### `searchForDeprecationInAliasesChain(symbol: ts.Symbol | undefined, checkDeprecationsOfAliasedSymbol: boolean): string | undefined`

<details><summary>Code</summary>

```ts
function searchForDeprecationInAliasesChain(
      symbol: ts.Symbol | undefined,
      checkDeprecationsOfAliasedSymbol: boolean,
    ): string | undefined {
      if (!symbol || !tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.Alias)) {
        return checkDeprecationsOfAliasedSymbol
          ? getJsDocDeprecation(symbol)
          : undefined;
      }
      const targetSymbol = checker.getAliasedSymbol(symbol);
      while (tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.Alias)) {
        const reason = getJsDocDeprecation(symbol);
        if (reason != null) {
          return reason;
        }
        const immediateAliasedSymbol: ts.Symbol | undefined =
          symbol.getDeclarations() && checker.getImmediateAliasedSymbol(symbol);
        if (!immediateAliasedSymbol) {
          break;
        }
        symbol = immediateAliasedSymbol;
        if (checkDeprecationsOfAliasedSymbol && symbol === targetSymbol) {
          return getJsDocDeprecation(symbol);
        }
      }
      return undefined;
    }
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol | undefined`
  - `checkDeprecationsOfAliasedSymbol: boolean`
- **Return Type**: `string | undefined`
- **Calls**:
  - `tsutils.isSymbolFlagSet`
  - `getJsDocDeprecation`
  - `checker.getAliasedSymbol`
  - `symbol.getDeclarations`
  - `checker.getImmediateAliasedSymbol`
### `isDeclaration(node: IdentifierLike): boolean`

<details><summary>Code</summary>

```ts
function isDeclaration(node: IdentifierLike): boolean {
      const { parent } = node;

      switch (parent.type) {
        case AST_NODE_TYPES.ArrayPattern:
          return parent.elements.includes(node as TSESTree.Identifier);

        case AST_NODE_TYPES.ClassExpression:
        case AST_NODE_TYPES.ClassDeclaration:
        case AST_NODE_TYPES.VariableDeclarator:
        case AST_NODE_TYPES.TSEnumMember:
          return parent.id === node;

        case AST_NODE_TYPES.MethodDefinition:
        case AST_NODE_TYPES.PropertyDefinition:
        case AST_NODE_TYPES.AccessorProperty:
          return parent.key === node;

        case AST_NODE_TYPES.Property:
          // foo in "const { foo } = bar" will be processed twice, as parent.key
          // and parent.value. The second is treated as a declaration.
          if (parent.shorthand && parent.value === node) {
            return parent.parent.type === AST_NODE_TYPES.ObjectPattern;
          }
          if (parent.value === node) {
            return false;
          }
          return parent.parent.type === AST_NODE_TYPES.ObjectExpression;

        case AST_NODE_TYPES.AssignmentPattern:
          // foo in "const { foo = "" } = bar" will be processed twice, as parent.parent.key
          // and parent.left. The second is treated as a declaration.
          return parent.left === node;

        case AST_NODE_TYPES.ArrowFunctionExpression:
        case AST_NODE_TYPES.FunctionDeclaration:
        case AST_NODE_TYPES.FunctionExpression:
        case AST_NODE_TYPES.TSDeclareFunction:
        case AST_NODE_TYPES.TSEmptyBodyFunctionExpression:
        case AST_NODE_TYPES.TSEnumDeclaration:
        case AST_NODE_TYPES.TSInterfaceDeclaration:
        case AST_NODE_TYPES.TSMethodSignature:
        case AST_NODE_TYPES.TSModuleDeclaration:
        case AST_NODE_TYPES.TSParameterProperty:
        case AST_NODE_TYPES.TSPropertySignature:
        case AST_NODE_TYPES.TSTypeAliasDeclaration:
        case AST_NODE_TYPES.TSTypeParameter:
          return true;

        default:
          return false;
      }
    }
```
</details>

- **Parameters**:
  - `node: IdentifierLike`
- **Return Type**: `boolean`
- **Calls**:
  - `parent.elements.includes`
- **Internal Comments**:
```
// foo in "const { foo } = bar" will be processed twice, as parent.key
// and parent.value. The second is treated as a declaration.
// foo in "const { foo = "" } = bar" will be processed twice, as parent.parent.key
// and parent.left. The second is treated as a declaration.
```

### `isInsideExportOrImport(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function isInsideExportOrImport(node: TSESTree.Node): boolean {
      let current = node;

      while (true) {
        switch (current.type) {
          case AST_NODE_TYPES.ExportAllDeclaration:
          case AST_NODE_TYPES.ExportNamedDeclaration:
          case AST_NODE_TYPES.ImportDeclaration:
            return true;

          case AST_NODE_TYPES.ArrowFunctionExpression:
          case AST_NODE_TYPES.BlockStatement:
          case AST_NODE_TYPES.ClassDeclaration:
          case AST_NODE_TYPES.TSInterfaceDeclaration:
          case AST_NODE_TYPES.FunctionDeclaration:
          case AST_NODE_TYPES.FunctionExpression:
          case AST_NODE_TYPES.Program:
          case AST_NODE_TYPES.TSUnionType:
          case AST_NODE_TYPES.VariableDeclarator:
            return false;

          default:
            current = current.parent;
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `getJsDocDeprecation(symbol: ts.Signature | ts.Symbol | undefined): string | undefined`

<details><summary>Code</summary>

```ts
function getJsDocDeprecation(
      symbol: ts.Signature | ts.Symbol | undefined,
    ): string | undefined {
      let jsDocTags: ts.JSDocTagInfo[] | undefined;
      try {
        jsDocTags = symbol?.getJsDocTags(checker);
      } catch {
        // workaround for https://github.com/microsoft/TypeScript/issues/60024
        return;
      }
      const tag = jsDocTags?.find(tag => tag.name === 'deprecated');

      if (!tag) {
        return undefined;
      }

      const displayParts = tag.text;

      return displayParts ? ts.displayPartsToString(displayParts) : '';
    }
```
</details>

- **Parameters**:
  - `symbol: ts.Signature | ts.Symbol | undefined`
- **Return Type**: `string | undefined`
- **Calls**:
  - `symbol?.getJsDocTags`
  - `jsDocTags?.find`
  - `ts.displayPartsToString`
- **Internal Comments**:
```
// workaround for https://github.com/microsoft/TypeScript/issues/60024
```

### `isNodeCalleeOfParent(node: TSESTree.Node): node is CallLikeNode`

<details><summary>Code</summary>

```ts
function isNodeCalleeOfParent(node: TSESTree.Node): node is CallLikeNode {
      switch (node.parent?.type) {
        case AST_NODE_TYPES.NewExpression:
        case AST_NODE_TYPES.CallExpression:
          return node.parent.callee === node;

        case AST_NODE_TYPES.TaggedTemplateExpression:
          return node.parent.tag === node;

        case AST_NODE_TYPES.JSXOpeningElement:
          return node.parent.name === node;

        default:
          return false;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is CallLikeNode`
### `getCallLikeNode(node: TSESTree.Node): CallLikeNode | undefined`

<details><summary>Code</summary>

```ts
function getCallLikeNode(node: TSESTree.Node): CallLikeNode | undefined {
      let callee = node;

      while (
        callee.parent?.type === AST_NODE_TYPES.MemberExpression &&
        callee.parent.property === callee
      ) {
        callee = callee.parent;
      }

      return isNodeCalleeOfParent(callee) ? callee : undefined;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `CallLikeNode | undefined`
- **Calls**:
  - `isNodeCalleeOfParent`
### `getCallLikeDeprecation(node: CallLikeNode): string | undefined`

<details><summary>Code</summary>

```ts
function getCallLikeDeprecation(node: CallLikeNode): string | undefined {
      const tsNode = services.esTreeNodeToTSNodeMap.get(node.parent);

      // If the node is a direct function call, we look for its signature.
      const signature = nullThrows(
        checker.getResolvedSignature(tsNode as ts.CallLikeExpression),
        'Expected call like node to have signature',
      );

      const symbol = services.getSymbolAtLocation(node);
      const aliasedSymbol =
        symbol != null && tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.Alias)
          ? checker.getAliasedSymbol(symbol)
          : symbol;
      const symbolDeclarationKind = aliasedSymbol?.declarations?.[0].kind;
      // Properties with function-like types have "deprecated" jsdoc
      // on their symbols, not on their signatures:
      //
      // interface Props {
      //   /** @deprecated */
      //   property: () => 'foo'
      //   ^symbol^  ^signature^
      // }
      if (
        symbolDeclarationKind !== ts.SyntaxKind.MethodDeclaration &&
        symbolDeclarationKind !== ts.SyntaxKind.FunctionDeclaration &&
        symbolDeclarationKind !== ts.SyntaxKind.MethodSignature
      ) {
        return (
          searchForDeprecationInAliasesChain(symbol, true) ??
          getJsDocDeprecation(signature) ??
          getJsDocDeprecation(aliasedSymbol)
        );
      }
      return (
        searchForDeprecationInAliasesChain(
          symbol,
          // Here we're working with a function declaration or method.
          // Both can have 1 or more overloads, each overload creates one
          // ts.Declaration which is placed in symbol.declarations.
          //
          // Imagine the following code:
          //
          // function foo(): void
          // /** @deprecated Some Reason */
          // function foo(arg: string): void
          // function foo(arg?: string): void {}
          //
          // foo()    // <- foo is our symbol
          //
          // If we call getJsDocDeprecation(checker.getAliasedSymbol(symbol)),
          // we get 'Some Reason', but after all, we are calling foo with
          // a signature that is not deprecated!
          // It works this way because symbol.getJsDocTags returns tags from
          // all symbol declarations combined into one array. And AFAIK there is
          // no publicly exported TS function that can tell us if a particular
          // declaration is deprecated or not.
          //
          // So, in case of function and method declarations, we don't check original
          // aliased symbol, but rely on the getJsDocDeprecation(signature) call below.
          false,
        ) ?? getJsDocDeprecation(signature)
      );
    }
```
</details>

- **Parameters**:
  - `node: CallLikeNode`
- **Return Type**: `string | undefined`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `nullThrows (from ../util)`
  - `checker.getResolvedSignature`
  - `services.getSymbolAtLocation`
  - `tsutils.isSymbolFlagSet`
  - `checker.getAliasedSymbol`
  - `searchForDeprecationInAliasesChain`
  - `getJsDocDeprecation`
- **Internal Comments**:
```
// If the node is a direct function call, we look for its signature. (x2)
// Properties with function-like types have "deprecated" jsdoc
// on their symbols, not on their signatures:
// (x6)
// interface Props {
//   /** @deprecated */
//   property: () => 'foo'
//   ^symbol^  ^signature^
// }
// Here we're working with a function declaration or method.
// Both can have 1 or more overloads, each overload creates one
// ts.Declaration which is placed in symbol.declarations.
// Imagine the following code:
// function foo(): void
// /** @deprecated Some Reason */
// function foo(arg: string): void
// function foo(arg?: string): void {}
// foo()    // <- foo is our symbol
// If we call getJsDocDeprecation(checker.getAliasedSymbol(symbol)),
// we get 'Some Reason', but after all, we are calling foo with
// a signature that is not deprecated!
// It works this way because symbol.getJsDocTags returns tags from
// all symbol declarations combined into one array. And AFAIK there is
// no publicly exported TS function that can tell us if a particular
// declaration is deprecated or not.
// So, in case of function and method declarations, we don't check original
// aliased symbol, but rely on the getJsDocDeprecation(signature) call below.
```

### `getJSXAttributeDeprecation(openingElement: TSESTree.JSXOpeningElement, propertyName: string): string | undefined`

<details><summary>Code</summary>

```ts
function getJSXAttributeDeprecation(
      openingElement: TSESTree.JSXOpeningElement,
      propertyName: string,
    ): string | undefined {
      const tsNode = services.esTreeNodeToTSNodeMap.get(openingElement.name);

      const contextualType = nullThrows(
        checker.getContextualType(tsNode as ts.Expression),
        'Expected JSX opening element name to have contextualType',
      );

      const symbol = contextualType.getProperty(propertyName);

      return getJsDocDeprecation(symbol);
    }
```
</details>

- **Parameters**:
  - `openingElement: TSESTree.JSXOpeningElement`
  - `propertyName: string`
- **Return Type**: `string | undefined`
- **Calls**:
  - `services.esTreeNodeToTSNodeMap.get`
  - `nullThrows (from ../util)`
  - `checker.getContextualType`
  - `contextualType.getProperty`
  - `getJsDocDeprecation`
### `getDeprecationReason(node: IdentifierLike): string | undefined`

<details><summary>Code</summary>

```ts
function getDeprecationReason(node: IdentifierLike): string | undefined {
      const callLikeNode = getCallLikeNode(node);
      if (callLikeNode) {
        return getCallLikeDeprecation(callLikeNode);
      }

      if (
        node.parent.type === AST_NODE_TYPES.JSXAttribute &&
        node.type !== AST_NODE_TYPES.Super
      ) {
        return getJSXAttributeDeprecation(node.parent.parent, node.name);
      }

      if (
        node.parent.type === AST_NODE_TYPES.Property &&
        node.type !== AST_NODE_TYPES.Super
      ) {
        const property = services
          .getTypeAtLocation(node.parent.parent)
          .getProperty(node.name);
        const propertySymbol = services.getSymbolAtLocation(node);
        const valueSymbol = checker.getShorthandAssignmentValueSymbol(
          propertySymbol?.valueDeclaration,
        );
        return (
          searchForDeprecationInAliasesChain(propertySymbol, true) ??
          getJsDocDeprecation(property) ??
          getJsDocDeprecation(propertySymbol) ??
          getJsDocDeprecation(valueSymbol)
        );
      }

      return searchForDeprecationInAliasesChain(
        services.getSymbolAtLocation(node),
        true,
      );
    }
```
</details>

- **Parameters**:
  - `node: IdentifierLike`
- **Return Type**: `string | undefined`
- **Calls**:
  - `getCallLikeNode`
  - `getCallLikeDeprecation`
  - `getJSXAttributeDeprecation`
  - `services
          .getTypeAtLocation(node.parent.parent)
          .getProperty`
  - `services.getSymbolAtLocation`
  - `checker.getShorthandAssignmentValueSymbol`
  - `searchForDeprecationInAliasesChain`
  - `getJsDocDeprecation`
### `checkIdentifier(node: IdentifierLike): void`

<details><summary>Code</summary>

```ts
function checkIdentifier(node: IdentifierLike): void {
      if (isDeclaration(node) || isInsideExportOrImport(node)) {
        return;
      }

      const reason = getDeprecationReason(node);
      if (reason == null) {
        return;
      }

      const type = services.getTypeAtLocation(node);
      if (typeMatchesSomeSpecifier(type, allow, services.program)) {
        return;
      }

      const name = getReportedNodeName(node);

      context.report({
        ...(reason
          ? {
              messageId: 'deprecatedWithReason',
              data: { name, reason },
            }
          : {
              messageId: 'deprecated',
              data: { name },
            }),
        node,
      });
    }
```
</details>

- **Parameters**:
  - `node: IdentifierLike`
- **Return Type**: `void`
- **Calls**:
  - `isDeclaration`
  - `isInsideExportOrImport`
  - `getDeprecationReason`
  - `services.getTypeAtLocation`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `getReportedNodeName`
  - `context.report`
### `checkMemberExpression(node: TSESTree.MemberExpression): void`

<details><summary>Code</summary>

```ts
function checkMemberExpression(node: TSESTree.MemberExpression): void {
      if (!node.computed) {
        return;
      }

      const propertyType = services.getTypeAtLocation(node.property);

      if (propertyType.isLiteral()) {
        const objectType = services.getTypeAtLocation(node.object);

        const propertyName = propertyType.isStringLiteral()
          ? propertyType.value
          : String(propertyType.value as number);

        const property = objectType.getProperty(propertyName);

        const reason = getJsDocDeprecation(property);
        if (reason == null) {
          return;
        }

        if (typeMatchesSomeSpecifier(objectType, allow, services.program)) {
          return;
        }

        context.report({
          ...(reason
            ? {
                messageId: 'deprecatedWithReason',
                data: { name: propertyName, reason },
              }
            : {
                messageId: 'deprecated',
                data: { name: propertyName },
              }),
          node: node.property,
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.MemberExpression`
- **Return Type**: `void`
- **Calls**:
  - `services.getTypeAtLocation`
  - `propertyType.isLiteral`
  - `propertyType.isStringLiteral`
  - `String`
  - `objectType.getProperty`
  - `getJsDocDeprecation`
  - `typeMatchesSomeSpecifier (from ../util)`
  - `context.report`
### `getReportedNodeName(node: IdentifierLike): string`

<details><summary>Code</summary>

```ts
function getReportedNodeName(node: IdentifierLike): string {
  if (node.type === AST_NODE_TYPES.Super) {
    return 'super';
  }

  if (node.type === AST_NODE_TYPES.PrivateIdentifier) {
    return `#${node.name}`;
  }

  return node.name;
}
```
</details>

- **Parameters**:
  - `node: IdentifierLike`
- **Return Type**: `string`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

### `IdentifierLike`

```ts
type IdentifierLike = | TSESTree.Identifier
  | TSESTree.JSXIdentifier
  | TSESTree.PrivateIdentifier
  | TSESTree.Super;
```

### `MessageIds`

```ts
type MessageIds = 'deprecated' | 'deprecatedWithReason';
```

### `Options`

```ts
type Options = [
  {
    allow?: TypeOrValueSpecifier[];
  },
];
```

### `CallLikeNode`

```ts
type CallLikeNode = | TSESTree.CallExpression
      | TSESTree.JSXOpeningElement
      | TSESTree.NewExpression
      | TSESTree.TaggedTemplateExpression;
```


---