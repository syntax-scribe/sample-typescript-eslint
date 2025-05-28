[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-qualifier.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 11 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 5 |
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

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-qualifier.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `namespacesInScope` | `ts.Node[]` | const | `[]` | ✗ |
| `currentFailedNamespaceExpression` | `TSESTree.Node | null` | let/var | `null` | ✗ |
| `esTreeNodeToTSNodeMap` | `any` | const | `services.esTreeNodeToTSNodeMap` | ✗ |
| `symbolDeclarations` | `any` | const | `symbol.getDeclarations() ?? []` | ✗ |
| `property` | `TSESTree.Identifier` | const | `node.property as TSESTree.Identifier` | ✗ |


---

## Functions

### `tryGetAliasedSymbol(symbol: ts.Symbol, checker: ts.TypeChecker): ts.Symbol | null`

<details><summary>Code</summary>

```ts
function tryGetAliasedSymbol(
      symbol: ts.Symbol,
      checker: ts.TypeChecker,
    ): ts.Symbol | null {
      return tsutils.isSymbolFlagSet(symbol, ts.SymbolFlags.Alias)
        ? checker.getAliasedSymbol(symbol)
        : null;
    }
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
  - `checker: ts.TypeChecker`
- **Return Type**: `ts.Symbol | null`
- **Calls**:
  - `tsutils.isSymbolFlagSet`
  - `checker.getAliasedSymbol`
### `symbolIsNamespaceInScope(symbol: ts.Symbol): boolean`

<details><summary>Code</summary>

```ts
function symbolIsNamespaceInScope(symbol: ts.Symbol): boolean {
      const symbolDeclarations = symbol.getDeclarations() ?? [];

      if (
        symbolDeclarations.some(decl =>
          namespacesInScope.some(ns => ns === decl),
        )
      ) {
        return true;
      }

      const alias = tryGetAliasedSymbol(symbol, checker);

      return alias != null && symbolIsNamespaceInScope(alias);
    }
```
</details>

- **Parameters**:
  - `symbol: ts.Symbol`
- **Return Type**: `boolean`
- **Calls**:
  - `symbol.getDeclarations`
  - `symbolDeclarations.some`
  - `namespacesInScope.some`
  - `tryGetAliasedSymbol`
  - `symbolIsNamespaceInScope`
### `getSymbolInScope(node: ts.Node, flags: ts.SymbolFlags, name: string): ts.Symbol | undefined`

<details><summary>Code</summary>

```ts
function getSymbolInScope(
      node: ts.Node,
      flags: ts.SymbolFlags,
      name: string,
    ): ts.Symbol | undefined {
      const scope = checker.getSymbolsInScope(node, flags);

      return scope.find(scopeSymbol => scopeSymbol.name === name);
    }
```
</details>

- **Parameters**:
  - `node: ts.Node`
  - `flags: ts.SymbolFlags`
  - `name: string`
- **Return Type**: `ts.Symbol | undefined`
- **Calls**:
  - `checker.getSymbolsInScope`
  - `scope.find`
### `symbolsAreEqual(accessed: ts.Symbol, inScope: ts.Symbol): boolean`

<details><summary>Code</summary>

```ts
function symbolsAreEqual(accessed: ts.Symbol, inScope: ts.Symbol): boolean {
      return accessed === checker.getExportSymbolOfSymbol(inScope);
    }
```
</details>

- **Parameters**:
  - `accessed: ts.Symbol`
  - `inScope: ts.Symbol`
- **Return Type**: `boolean`
- **Calls**:
  - `checker.getExportSymbolOfSymbol`
### `qualifierIsUnnecessary(qualifier: TSESTree.EntityName | TSESTree.MemberExpression, name: TSESTree.Identifier): boolean`

<details><summary>Code</summary>

```ts
function qualifierIsUnnecessary(
      qualifier: TSESTree.EntityName | TSESTree.MemberExpression,
      name: TSESTree.Identifier,
    ): boolean {
      const namespaceSymbol = services.getSymbolAtLocation(qualifier);

      if (
        namespaceSymbol == null ||
        !symbolIsNamespaceInScope(namespaceSymbol)
      ) {
        return false;
      }

      const accessedSymbol = services.getSymbolAtLocation(name);

      if (accessedSymbol == null) {
        return false;
      }

      // If the symbol in scope is different, the qualifier is necessary.
      const tsQualifier = esTreeNodeToTSNodeMap.get(qualifier);
      const fromScope = getSymbolInScope(
        tsQualifier,
        accessedSymbol.flags,
        context.sourceCode.getText(name),
      );

      return !!fromScope && symbolsAreEqual(accessedSymbol, fromScope);
    }
```
</details>

- **Parameters**:
  - `qualifier: TSESTree.EntityName | TSESTree.MemberExpression`
  - `name: TSESTree.Identifier`
- **Return Type**: `boolean`
- **Calls**:
  - `services.getSymbolAtLocation`
  - `symbolIsNamespaceInScope`
  - `esTreeNodeToTSNodeMap.get`
  - `getSymbolInScope`
  - `context.sourceCode.getText`
  - `symbolsAreEqual`
- **Internal Comments**:
```
// If the symbol in scope is different, the qualifier is necessary. (x2)
```

### `visitNamespaceAccess(node: TSESTree.Node, qualifier: TSESTree.EntityName | TSESTree.MemberExpression, name: TSESTree.Identifier): void`

<details><summary>Code</summary>

```ts
function visitNamespaceAccess(
      node: TSESTree.Node,
      qualifier: TSESTree.EntityName | TSESTree.MemberExpression,
      name: TSESTree.Identifier,
    ): void {
      // Only look for nested qualifier errors if we didn't already fail on the outer qualifier.
      if (
        !currentFailedNamespaceExpression &&
        qualifierIsUnnecessary(qualifier, name)
      ) {
        currentFailedNamespaceExpression = node;
        context.report({
          node: qualifier,
          messageId: 'unnecessaryQualifier',
          data: {
            name: context.sourceCode.getText(name),
          },
          fix(fixer) {
            return fixer.removeRange([qualifier.range[0], name.range[0]]);
          },
        });
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `qualifier: TSESTree.EntityName | TSESTree.MemberExpression`
  - `name: TSESTree.Identifier`
- **Return Type**: `void`
- **Calls**:
  - `qualifierIsUnnecessary`
  - `context.report`
  - `context.sourceCode.getText`
  - `fixer.removeRange`
- **Internal Comments**:
```
// Only look for nested qualifier errors if we didn't already fail on the outer qualifier.
```

### `enterDeclaration(node: | TSESTree.ExportNamedDeclaration
        | TSESTree.TSEnumDeclaration
        | TSESTree.TSModuleDeclaration): void`

<details><summary>Code</summary>

```ts
function enterDeclaration(
      node:
        | TSESTree.ExportNamedDeclaration
        | TSESTree.TSEnumDeclaration
        | TSESTree.TSModuleDeclaration,
    ): void {
      namespacesInScope.push(esTreeNodeToTSNodeMap.get(node));
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ExportNamedDeclaration
        | TSESTree.TSEnumDeclaration
        | TSESTree.TSModuleDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `namespacesInScope.push`
  - `esTreeNodeToTSNodeMap.get`
### `exitDeclaration(): void`

<details><summary>Code</summary>

```ts
function exitDeclaration(): void {
      namespacesInScope.pop();
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `namespacesInScope.pop`
### `resetCurrentNamespaceExpression(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function resetCurrentNamespaceExpression(node: TSESTree.Node): void {
      if (node === currentFailedNamespaceExpression) {
        currentFailedNamespaceExpression = null;
      }
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
### `isPropertyAccessExpression(node: TSESTree.Node): node is TSESTree.MemberExpression`

<details><summary>Code</summary>

```ts
function isPropertyAccessExpression(
      node: TSESTree.Node,
    ): node is TSESTree.MemberExpression {
      return node.type === AST_NODE_TYPES.MemberExpression && !node.computed;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.MemberExpression`
### `isEntityNameExpression(node: TSESTree.Node): node is TSESTree.Identifier | TSESTree.MemberExpression`

<details><summary>Code</summary>

```ts
function isEntityNameExpression(
      node: TSESTree.Node,
    ): node is TSESTree.Identifier | TSESTree.MemberExpression {
      return (
        node.type === AST_NODE_TYPES.Identifier ||
        (isPropertyAccessExpression(node) &&
          isEntityNameExpression(node.object))
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.Identifier | TSESTree.MemberExpression`
- **Calls**:
  - `isPropertyAccessExpression`
  - `isEntityNameExpression`

---