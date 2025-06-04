[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-redeclare.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 3 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 6 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-redeclare.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ScopeType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getNameLocationInGlobalDirectiveComment` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `CLASS_DECLARATION_MERGE_NODES` | `Set<AST_NODE_TYPES>` | const | `new Set<AST_NODE_TYPES>([
      AST_NODE_TYPES.ClassDeclaration,
      AST_NODE_TYPES.TSInterfaceDeclaration,
      AST_NODE_TYPES.TSModuleDeclaration,
    ])` | ✗ |
| `FUNCTION_DECLARATION_MERGE_NODES` | `Set<AST_NODE_TYPES>` | const | `new Set<AST_NODE_TYPES>([
      AST_NODE_TYPES.FunctionDeclaration,
      AST_NODE_TYPES.TSModuleDeclaration,
    ])` | ✗ |
| `ENUM_DECLARATION_MERGE_NODES` | `Set<AST_NODE_TYPES>` | const | `new Set<AST_NODE_TYPES>([
      AST_NODE_TYPES.TSEnumDeclaration,
      AST_NODE_TYPES.TSModuleDeclaration,
    ])` | ✗ |
| `detailMessageId` | `"redeclaredAsBuiltin" | "redeclaredBySyntax"` | const | `declaration.type === 'builtin'
            ? 'redeclaredAsBuiltin'
            : 'redeclaredBySyntax'` | ✗ |
| `data` | `{ id: any; }` | const | `{ id: variable.name }` | ✗ |
| `messageId` | `"redeclaredAsBuiltin" | "redeclaredBySyntax" | "redeclared"` | const | `type === declaration.type ? 'redeclared' : detailMessageId` | ✗ |


---

## Functions

### `iterateDeclarations(variable: TSESLint.Scope.Variable): Generator<
      {
        loc?: TSESTree.SourceLocation;
        node?: TSESTree.Comment | TSESTree.Identifier;
        type: 'builtin' | 'comment' | 'syntax';
      },
      void
    >`

<details><summary>Code</summary>

```ts
function* iterateDeclarations(variable: TSESLint.Scope.Variable): Generator<
      {
        loc?: TSESTree.SourceLocation;
        node?: TSESTree.Comment | TSESTree.Identifier;
        type: 'builtin' | 'comment' | 'syntax';
      },
      void
    > {
      if (
        options.builtinGlobals &&
        'eslintImplicitGlobalSetting' in variable &&
        (variable.eslintImplicitGlobalSetting === 'readonly' ||
          variable.eslintImplicitGlobalSetting === 'writable')
      ) {
        yield { type: 'builtin' };
      }

      if (
        'eslintExplicitGlobalComments' in variable &&
        variable.eslintExplicitGlobalComments
      ) {
        for (const comment of variable.eslintExplicitGlobalComments) {
          yield {
            loc: getNameLocationInGlobalDirectiveComment(
              context.sourceCode,
              comment,
              variable.name,
            ),
            node: comment,
            type: 'comment',
          };
        }
      }

      const identifiers = variable.identifiers
        .map(id => ({
          identifier: id,
          parent: id.parent,
        }))
        // ignore function declarations because TS will treat them as an overload
        .filter(
          ({ parent }) => parent.type !== AST_NODE_TYPES.TSDeclareFunction,
        );

      if (options.ignoreDeclarationMerge && identifiers.length > 1) {
        if (
          // interfaces merging
          identifiers.every(
            ({ parent }) =>
              parent.type === AST_NODE_TYPES.TSInterfaceDeclaration,
          )
        ) {
          return;
        }

        if (
          // namespace/module merging
          identifiers.every(
            ({ parent }) => parent.type === AST_NODE_TYPES.TSModuleDeclaration,
          )
        ) {
          return;
        }

        if (
          // class + interface/namespace merging
          identifiers.every(({ parent }) =>
            CLASS_DECLARATION_MERGE_NODES.has(parent.type),
          )
        ) {
          const classDecls = identifiers.filter(
            ({ parent }) => parent.type === AST_NODE_TYPES.ClassDeclaration,
          );
          if (classDecls.length === 1) {
            // safe declaration merging
            return;
          }

          // there's more than one class declaration, which needs to be reported
          for (const { identifier } of classDecls) {
            yield { loc: identifier.loc, node: identifier, type: 'syntax' };
          }
          return;
        }

        if (
          // class + interface/namespace merging
          identifiers.every(({ parent }) =>
            FUNCTION_DECLARATION_MERGE_NODES.has(parent.type),
          )
        ) {
          const functionDecls = identifiers.filter(
            ({ parent }) => parent.type === AST_NODE_TYPES.FunctionDeclaration,
          );
          if (functionDecls.length === 1) {
            // safe declaration merging
            return;
          }

          // there's more than one function declaration, which needs to be reported
          for (const { identifier } of functionDecls) {
            yield { loc: identifier.loc, node: identifier, type: 'syntax' };
          }
          return;
        }

        if (
          // enum + namespace merging
          identifiers.every(({ parent }) =>
            ENUM_DECLARATION_MERGE_NODES.has(parent.type),
          )
        ) {
          const enumDecls = identifiers.filter(
            ({ parent }) => parent.type === AST_NODE_TYPES.TSEnumDeclaration,
          );
          if (enumDecls.length === 1) {
            // safe declaration merging
            return;
          }

          // there's more than one enum declaration, which needs to be reported
          for (const { identifier } of enumDecls) {
            yield { loc: identifier.loc, node: identifier, type: 'syntax' };
          }
          return;
        }
      }

      for (const { identifier } of identifiers) {
        yield { loc: identifier.loc, node: identifier, type: 'syntax' };
      }
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `Generator<
      {
        loc?: TSESTree.SourceLocation;
        node?: TSESTree.Comment | TSESTree.Identifier;
        type: 'builtin' | 'comment' | 'syntax';
      },
      void
    >`
- **Calls**:
  - `getNameLocationInGlobalDirectiveComment (from ../util)`
  - `variable.identifiers
        .map(id => ({
          identifier: id,
          parent: id.parent,
        }))
        // ignore function declarations because TS will treat them as an overload
        .filter`
  - `identifiers.every`
  - `CLASS_DECLARATION_MERGE_NODES.has`
  - `identifiers.filter`
  - `FUNCTION_DECLARATION_MERGE_NODES.has`
  - `ENUM_DECLARATION_MERGE_NODES.has`
- **Internal Comments**:
```
// interfaces merging (x3)
// namespace/module merging (x3)
// class + interface/namespace merging (x6)
// safe declaration merging (x3)
// there's more than one class declaration, which needs to be reported
// there's more than one function declaration, which needs to be reported
// enum + namespace merging (x3)
// there's more than one enum declaration, which needs to be reported
```

### `findVariablesInScope(scope: TSESLint.Scope.Scope): void`

<details><summary>Code</summary>

```ts
function findVariablesInScope(scope: TSESLint.Scope.Scope): void {
      for (const variable of scope.variables) {
        const [declaration, ...extraDeclarations] =
          iterateDeclarations(variable);

        if (extraDeclarations.length === 0) {
          continue;
        }

        /*
         * If the type of a declaration is different from the type of
         * the first declaration, it shows the location of the first
         * declaration.
         */
        const detailMessageId =
          declaration.type === 'builtin'
            ? 'redeclaredAsBuiltin'
            : 'redeclaredBySyntax';
        const data = { id: variable.name };

        // Report extra declarations.
        for (const { loc, node, type } of extraDeclarations) {
          const messageId =
            type === declaration.type ? 'redeclared' : detailMessageId;

          if (node) {
            context.report({ loc, node, messageId, data });
          } else if (loc) {
            context.report({ loc, messageId, data });
          }
        }
      }
    }
```
</details>

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
- **Return Type**: `void`
- **Calls**:
  - `iterateDeclarations`
  - `context.report`
- **Internal Comments**:
```
/*
         * If the type of a declaration is different from the type of
         * the first declaration, it shows the location of the first
         * declaration.
         */ (x2)
// Report extra declarations.
```

### `checkForBlock(node: TSESTree.Node): void`

<details><summary>Code</summary>

```ts
function checkForBlock(node: TSESTree.Node): void {
      const scope = context.sourceCode.getScope(node);

      /*
       * In ES5, some node type such as `BlockStatement` doesn't have that scope.
       * `scope.block` is a different node in such a case.
       */
      if (scope.block === node) {
        findVariablesInScope(scope);
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Find variables in the current scope.
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `findVariablesInScope`
- **Internal Comments**:
```
/*
       * In ES5, some node type such as `BlockStatement` doesn't have that scope.
       * `scope.block` is a different node in such a case.
       */
```


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'redeclared'
  | 'redeclaredAsBuiltin'
  | 'redeclaredBySyntax';
```

### `Options`

```ts
type Options = [
  {
    builtinGlobals?: boolean;
    ignoreDeclarationMerge?: boolean;
  },
];
```


---