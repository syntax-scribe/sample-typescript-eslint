[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unused-vars.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 15 |
| 🧱 Classes | 0 |
| 📦 Imports | 16 |
| 📊 Variables & Constants | 21 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 5 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-unused-vars.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Definition` | `@typescript-eslint/scope-manager` |
| `ScopeVariable` | `@typescript-eslint/scope-manager` |
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `PatternVisitor` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TSESLint` | `@typescript-eslint/utils` |
| `MakeRequired` | `../util` |
| `collectVariables` | `../util` |
| `createRule` | `../util` |
| `getNameLocationInGlobalDirectiveComment` | `../util` |
| `isDefinitionFile` | `../util` |
| `isFunction` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |
| `referenceContainsTypeQuery` | `../util/referenceContainsTypeQuery` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `MODULE_DECL_CACHE` | `Map<any, boolean>` | const | `new Map<
      ModuleDeclarationWithBody | TSESTree.Program,
      boolean
    >()` | ✗ |
| `options` | `TranslatedOptions` | const | `{
        args: 'after-used',
        caughtErrors: 'all',
        ignoreClassWithStaticInitBlock: false,
        ignoreRestSiblings: false,
        reportUsedIgnorePattern: false,
        vars: 'all',
      }` | ✗ |
| `additionalMessageData` | `string` | let/var | `''` | ✗ |
| `additionalMessageData` | `string` | let/var | `''` | ✗ |
| `additionalMessageData` | `string` | let/var | `''` | ✗ |
| `def` | `any` | const | `variable.defs[0]` | ✗ |
| `variables` | `{ used: boolean; variable: ScopeVariable; }[]` | const | `[
        ...Array.from(analysisResults.unusedVariables, variable => ({
          used: false,
          variable,
        })),
        ...Array.from(analysisResults.usedVariables, variable => ({
          used: true,
          variable,
        })),
      ]` | ✗ |
| `unusedVariablesReturn` | `ScopeVariable[]` | const | `[]` | ✗ |
| `def` | `any` | const | `variable.defs[0]` | ✗ |
| `moduleDecl` | `TSESTree.Program` | const | `nullThrows(
          node.parent,
          NullThrowsReasons.MissingParent,
        ) as TSESTree.Program` | ✗ |
| `moduleDecl` | `ModuleDeclarationWithBody` | const | `nullThrows(
          node.parent.parent,
          NullThrowsReasons.MissingParent,
        ) as ModuleDeclarationWithBody` | ✗ |
| `moduleDecl` | `ModuleDeclarationWithBody` | const | `nullThrows(
          node.parent.parent,
          NullThrowsReasons.MissingParent,
        ) as ModuleDeclarationWithBody` | ✗ |
| `moduleDecl` | `ModuleDeclarationWithBody` | const | `nullThrows(
          node.parent.parent,
          NullThrowsReasons.MissingParent,
        ) as ModuleDeclarationWithBody` | ✗ |
| `isImportUsedOnlyAsType` | `any` | const | `usedOnlyAsType &&
              unusedVar.defs.some(
                def => def.type === DefinitionType.ImportBinding,
              )` | ✗ |
| `id` | `any` | const | `writeReferences.length
              ? writeReferences[writeReferences.length - 1].identifier
              : unusedVar.identifiers[0]` | ✗ |
| `messageId` | `"unusedVar" | "usedOnlyAsType"` | const | `usedOnlyAsType ? 'usedOnlyAsType' : 'unusedVar'` | ✗ |
| `idLength` | `any` | const | `id.name.length` | ✗ |
| `loc` | `{ start: any; end: { column: any; line: any; }; }` | const | `{
              start,
              end: {
                column: start.column + idLength,
                line: start.line,
              },
            }` | ✗ |
| `directiveComment` | `any` | const | `unusedVar.eslintExplicitGlobalComments[0]` | ✗ |
| `identifiers` | `TSESTree.Identifier[]` | const | `[]` | ✗ |
| `visitor` | `any` | const | `new PatternVisitor({}, node, cb)` | ✗ |


---

## Functions

### `defToVariableType(def: Definition): VariableType`

<details><summary>Code</summary>

```ts
function defToVariableType(def: Definition): VariableType {
      /*
       * This `destructuredArrayIgnorePattern` error report works differently from the catch
       * clause and parameter error reports. _Both_ the `varsIgnorePattern` and the
       * `destructuredArrayIgnorePattern` will be checked for array destructuring. However,
       * for the purposes of the report, the currently defined behavior is to only inform the
       * user of the `destructuredArrayIgnorePattern` if it's present (regardless of the fact
       * that the `varsIgnorePattern` would also apply). If it's not present, the user will be
       * informed of the `varsIgnorePattern`, assuming that's present.
       */
      if (
        options.destructuredArrayIgnorePattern &&
        def.name.parent.type === AST_NODE_TYPES.ArrayPattern
      ) {
        return 'array-destructure';
      }

      switch (def.type) {
        case DefinitionType.CatchClause:
          return 'catch-clause';
        case DefinitionType.Parameter:
          return 'parameter';
        default:
          return 'variable';
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Determines what variable type a def is.
     * @param def the declaration to check
     * @returns a simple name for the types of variables that this rule supports
     */
```

- **Parameters**:
  - `def: Definition`
- **Return Type**: `VariableType`
- **Internal Comments**:
```
/*
       * This `destructuredArrayIgnorePattern` error report works differently from the catch
       * clause and parameter error reports. _Both_ the `varsIgnorePattern` and the
       * `destructuredArrayIgnorePattern` will be checked for array destructuring. However,
       * for the purposes of the report, the currently defined behavior is to only inform the
       * user of the `destructuredArrayIgnorePattern` if it's present (regardless of the fact
       * that the `varsIgnorePattern` would also apply). If it's not present, the user will be
       * informed of the `varsIgnorePattern`, assuming that's present.
       */
```

### `getVariableDescription(variableType: VariableType): {
      pattern: string | undefined;
      variableDescription: string;
    }`

<details><summary>Code</summary>

```ts
function getVariableDescription(variableType: VariableType): {
      pattern: string | undefined;
      variableDescription: string;
    } {
      switch (variableType) {
        case 'array-destructure':
          return {
            pattern: options.destructuredArrayIgnorePattern?.toString(),
            variableDescription: 'elements of array destructuring',
          };

        case 'catch-clause':
          return {
            pattern: options.caughtErrorsIgnorePattern?.toString(),
            variableDescription: 'caught errors',
          };

        case 'parameter':
          return {
            pattern: options.argsIgnorePattern?.toString(),
            variableDescription: 'args',
          };

        case 'variable':
          return {
            pattern: options.varsIgnorePattern?.toString(),
            variableDescription: 'vars',
          };
      }
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Gets a given variable's description and configured ignore pattern
     * based on the provided variableType
     * @param variableType a simple name for the types of variables that this rule supports
     * @returns the given variable's description and
     * ignore pattern
     */
```

- **Parameters**:
  - `variableType: VariableType`
- **Return Type**: `{
      pattern: string | undefined;
      variableDescription: string;
    }`
- **Calls**:
  - `options.destructuredArrayIgnorePattern?.toString`
  - `options.caughtErrorsIgnorePattern?.toString`
  - `options.argsIgnorePattern?.toString`
  - `options.varsIgnorePattern?.toString`
### `getDefinedMessageData(unusedVar: ScopeVariable): Record<string, unknown>`

<details><summary>Code</summary>

```ts
function getDefinedMessageData(
      unusedVar: ScopeVariable,
    ): Record<string, unknown> {
      const def = unusedVar.defs.at(0);
      let additionalMessageData = '';

      if (def) {
        const { pattern, variableDescription } = getVariableDescription(
          defToVariableType(def),
        );

        if (pattern && variableDescription) {
          additionalMessageData = `. Allowed unused ${variableDescription} must match ${pattern}`;
        }
      }

      return {
        action: 'defined',
        additional: additionalMessageData,
        varName: unusedVar.name,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Generates the message data about the variable being defined and unused,
     * including the ignore pattern if configured.
     * @param unusedVar eslint-scope variable object.
     * @returns The message data to be used with this unused variable.
     */
```

- **Parameters**:
  - `unusedVar: ScopeVariable`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `unusedVar.defs.at`
  - `getVariableDescription`
  - `defToVariableType`
### `getAssignedMessageData(unusedVar: ScopeVariable): Record<string, unknown>`

<details><summary>Code</summary>

```ts
function getAssignedMessageData(
      unusedVar: ScopeVariable,
    ): Record<string, unknown> {
      const def = unusedVar.defs.at(0);
      let additionalMessageData = '';

      if (def) {
        const { pattern, variableDescription } = getVariableDescription(
          defToVariableType(def),
        );

        if (pattern && variableDescription) {
          additionalMessageData = `. Allowed unused ${variableDescription} must match ${pattern}`;
        }
      }

      return {
        action: 'assigned a value',
        additional: additionalMessageData,
        varName: unusedVar.name,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Generate the warning message about the variable being
     * assigned and unused, including the ignore pattern if configured.
     * @param unusedVar eslint-scope variable object.
     * @returns The message data to be used with this unused variable.
     */
```

- **Parameters**:
  - `unusedVar: ScopeVariable`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `unusedVar.defs.at`
  - `getVariableDescription`
  - `defToVariableType`
### `getUsedIgnoredMessageData(variable: ScopeVariable, variableType: VariableType): Record<string, unknown>`

<details><summary>Code</summary>

```ts
function getUsedIgnoredMessageData(
      variable: ScopeVariable,
      variableType: VariableType,
    ): Record<string, unknown> {
      const { pattern, variableDescription } =
        getVariableDescription(variableType);

      let additionalMessageData = '';

      if (pattern && variableDescription) {
        additionalMessageData = `. Used ${variableDescription} must not match ${pattern}`;
      }

      return {
        additional: additionalMessageData,
        varName: variable.name,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Generate the warning message about a variable being used even though
     * it is marked as being ignored.
     * @param variable eslint-scope variable object
     * @param variableType a simple name for the types of variables that this rule supports
     * @returns The message data to be used with this used ignored variable.
     */
```

- **Parameters**:
  - `variable: ScopeVariable`
  - `variableType: VariableType`
- **Return Type**: `Record<string, unknown>`
- **Calls**:
  - `getVariableDescription`
### `collectUnusedVariables(): ScopeVariable[]`

<details><summary>Code</summary>

```ts
function collectUnusedVariables(): ScopeVariable[] {
      /**
       * Checks whether a node is a sibling of the rest property or not.
       * @param node a node to check
       * @returns True if the node is a sibling of the rest property, otherwise false.
       */
      function hasRestSibling(node: TSESTree.Node): boolean {
        return (
          node.type === AST_NODE_TYPES.Property &&
          node.parent.type === AST_NODE_TYPES.ObjectPattern &&
          node.parent.properties[node.parent.properties.length - 1].type ===
            AST_NODE_TYPES.RestElement
        );
      }

      /**
       * Determines if a variable has a sibling rest property
       * @param variable eslint-scope variable object.
       * @returns True if the variable is exported, false if not.
       */
      function hasRestSpreadSibling(variable: ScopeVariable): boolean {
        if (options.ignoreRestSiblings) {
          const hasRestSiblingDefinition = variable.defs.some(def =>
            hasRestSibling(def.name.parent),
          );
          const hasRestSiblingReference = variable.references.some(ref =>
            hasRestSibling(ref.identifier.parent),
          );

          return hasRestSiblingDefinition || hasRestSiblingReference;
        }

        return false;
      }

      /**
       * Checks whether the given variable is after the last used parameter.
       * @param variable The variable to check.
       * @returns `true` if the variable is defined after the last used parameter.
       */
      function isAfterLastUsedArg(variable: ScopeVariable): boolean {
        const def = variable.defs[0];
        const params = context.sourceCode.getDeclaredVariables(def.node);
        const posteriorParams = params.slice(params.indexOf(variable) + 1);

        // If any used parameters occur after this parameter, do not report.
        return !posteriorParams.some(
          v => v.references.length > 0 || v.eslintUsed,
        );
      }

      const analysisResults = collectVariables(context);
      const variables = [
        ...Array.from(analysisResults.unusedVariables, variable => ({
          used: false,
          variable,
        })),
        ...Array.from(analysisResults.usedVariables, variable => ({
          used: true,
          variable,
        })),
      ];
      const unusedVariablesReturn: ScopeVariable[] = [];
      for (const { used, variable } of variables) {
        // explicit global variables don't have definitions.
        if (variable.defs.length === 0) {
          if (!used) {
            unusedVariablesReturn.push(variable);
          }

          continue;
        }
        const def = variable.defs[0];

        if (
          variable.scope.type === TSESLint.Scope.ScopeType.global &&
          options.vars === 'local'
        ) {
          // skip variables in the global scope if configured to
          continue;
        }

        const refUsedInArrayPatterns = variable.references.some(
          ref => ref.identifier.parent.type === AST_NODE_TYPES.ArrayPattern,
        );

        // skip elements of array destructuring patterns
        if (
          (def.name.parent.type === AST_NODE_TYPES.ArrayPattern ||
            refUsedInArrayPatterns) &&
          def.name.type === AST_NODE_TYPES.Identifier &&
          options.destructuredArrayIgnorePattern?.test(def.name.name)
        ) {
          if (options.reportUsedIgnorePattern && used) {
            context.report({
              node: def.name,
              messageId: 'usedIgnoredVar',
              data: getUsedIgnoredMessageData(variable, 'array-destructure'),
            });
          }
          continue;
        }

        if (def.type === TSESLint.Scope.DefinitionType.ClassName) {
          const hasStaticBlock = def.node.body.body.some(
            node => node.type === AST_NODE_TYPES.StaticBlock,
          );

          if (options.ignoreClassWithStaticInitBlock && hasStaticBlock) {
            continue;
          }
        }

        // skip catch variables
        if (def.type === TSESLint.Scope.DefinitionType.CatchClause) {
          if (options.caughtErrors === 'none') {
            continue;
          }
          // skip ignored parameters
          if (
            def.name.type === AST_NODE_TYPES.Identifier &&
            options.caughtErrorsIgnorePattern?.test(def.name.name)
          ) {
            if (options.reportUsedIgnorePattern && used) {
              context.report({
                node: def.name,
                messageId: 'usedIgnoredVar',
                data: getUsedIgnoredMessageData(variable, 'catch-clause'),
              });
            }
            continue;
          }
        } else if (def.type === TSESLint.Scope.DefinitionType.Parameter) {
          // if "args" option is "none", skip any parameter
          if (options.args === 'none') {
            continue;
          }
          // skip ignored parameters
          if (
            def.name.type === AST_NODE_TYPES.Identifier &&
            options.argsIgnorePattern?.test(def.name.name)
          ) {
            if (options.reportUsedIgnorePattern && used) {
              context.report({
                node: def.name,
                messageId: 'usedIgnoredVar',
                data: getUsedIgnoredMessageData(variable, 'parameter'),
              });
            }
            continue;
          }
          // if "args" option is "after-used", skip used variables
          if (
            options.args === 'after-used' &&
            isFunction(def.name.parent) &&
            !isAfterLastUsedArg(variable)
          ) {
            continue;
          }
        }
        // skip ignored variables
        else if (
          def.name.type === AST_NODE_TYPES.Identifier &&
          options.varsIgnorePattern?.test(def.name.name)
        ) {
          if (
            options.reportUsedIgnorePattern &&
            used &&
            /* enum members are always marked as 'used' by `collectVariables`, but in reality they may be used or
               unused. either way, don't complain about their naming. */
            def.type !== TSESLint.Scope.DefinitionType.TSEnumMember
          ) {
            context.report({
              node: def.name,
              messageId: 'usedIgnoredVar',
              data: getUsedIgnoredMessageData(variable, 'variable'),
            });
          }
          continue;
        }

        if (hasRestSpreadSibling(variable)) {
          continue;
        }

        // in case another rule has run and used the collectUnusedVariables,
        // we want to ensure our selectors that marked variables as used are respected
        if (variable.eslintUsed) {
          continue;
        }

        if (!used) {
          unusedVariablesReturn.push(variable);
        }
      }

      return unusedVariablesReturn;
    }
```
</details>

- **Return Type**: `ScopeVariable[]`
- **Calls**:
  - `variable.defs.some`
  - `hasRestSibling`
  - `variable.references.some`
  - `context.sourceCode.getDeclaredVariables`
  - `params.slice`
  - `params.indexOf`
  - `posteriorParams.some`
  - `collectVariables (from ../util)`
  - `Array.from`
  - `unusedVariablesReturn.push`
  - `options.destructuredArrayIgnorePattern?.test`
  - `context.report`
  - `getUsedIgnoredMessageData`
  - `def.node.body.body.some`
  - `options.caughtErrorsIgnorePattern?.test`
  - `options.argsIgnorePattern?.test`
  - `isFunction (from ../util)`
  - `isAfterLastUsedArg`
  - `options.varsIgnorePattern?.test`
  - `hasRestSpreadSibling`
- **Internal Comments**:
```
/**
       * Checks whether a node is a sibling of the rest property or not.
       * @param node a node to check
       * @returns True if the node is a sibling of the rest property, otherwise false.
       */
/**
       * Determines if a variable has a sibling rest property
       * @param variable eslint-scope variable object.
       * @returns True if the variable is exported, false if not.
       */
/**
       * Checks whether the given variable is after the last used parameter.
       * @param variable The variable to check.
       * @returns `true` if the variable is defined after the last used parameter.
       */
// If any used parameters occur after this parameter, do not report.
// explicit global variables don't have definitions.
// skip variables in the global scope if configured to
// skip elements of array destructuring patterns
// skip catch variables
// skip ignored parameters (x2)
// if "args" option is "none", skip any parameter
// if "args" option is "after-used", skip used variables
/* enum members are always marked as 'used' by `collectVariables`, but in reality they may be used or
               unused. either way, don't complain about their naming. */ (x3)
// in case another rule has run and used the collectUnusedVariables,
// we want to ensure our selectors that marked variables as used are respected
```

### `hasRestSibling(node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function hasRestSibling(node: TSESTree.Node): boolean {
        return (
          node.type === AST_NODE_TYPES.Property &&
          node.parent.type === AST_NODE_TYPES.ObjectPattern &&
          node.parent.properties[node.parent.properties.length - 1].type ===
            AST_NODE_TYPES.RestElement
        );
      }
```
</details>

- **JSDoc**:
```ts
/**
       * Checks whether a node is a sibling of the rest property or not.
       * @param node a node to check
       * @returns True if the node is a sibling of the rest property, otherwise false.
       */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
### `hasRestSpreadSibling(variable: ScopeVariable): boolean`

<details><summary>Code</summary>

```ts
function hasRestSpreadSibling(variable: ScopeVariable): boolean {
        if (options.ignoreRestSiblings) {
          const hasRestSiblingDefinition = variable.defs.some(def =>
            hasRestSibling(def.name.parent),
          );
          const hasRestSiblingReference = variable.references.some(ref =>
            hasRestSibling(ref.identifier.parent),
          );

          return hasRestSiblingDefinition || hasRestSiblingReference;
        }

        return false;
      }
```
</details>

- **JSDoc**:
```ts
/**
       * Determines if a variable has a sibling rest property
       * @param variable eslint-scope variable object.
       * @returns True if the variable is exported, false if not.
       */
```

- **Parameters**:
  - `variable: ScopeVariable`
- **Return Type**: `boolean`
- **Calls**:
  - `variable.defs.some`
  - `hasRestSibling`
  - `variable.references.some`
### `isAfterLastUsedArg(variable: ScopeVariable): boolean`

<details><summary>Code</summary>

```ts
function isAfterLastUsedArg(variable: ScopeVariable): boolean {
        const def = variable.defs[0];
        const params = context.sourceCode.getDeclaredVariables(def.node);
        const posteriorParams = params.slice(params.indexOf(variable) + 1);

        // If any used parameters occur after this parameter, do not report.
        return !posteriorParams.some(
          v => v.references.length > 0 || v.eslintUsed,
        );
      }
```
</details>

- **JSDoc**:
```ts
/**
       * Checks whether the given variable is after the last used parameter.
       * @param variable The variable to check.
       * @returns `true` if the variable is defined after the last used parameter.
       */
```

- **Parameters**:
  - `variable: ScopeVariable`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getDeclaredVariables`
  - `params.slice`
  - `params.indexOf`
  - `posteriorParams.some`
- **Internal Comments**:
```
// If any used parameters occur after this parameter, do not report.
```

### `checkForOverridingExportStatements(node: ModuleDeclarationWithBody | TSESTree.Program): boolean`

<details><summary>Code</summary>

```ts
function checkForOverridingExportStatements(
      node: ModuleDeclarationWithBody | TSESTree.Program,
    ): boolean {
      const cached = MODULE_DECL_CACHE.get(node);
      if (cached != null) {
        return cached;
      }

      const body = getStatementsOfNode(node);

      if (hasOverridingExportStatement(body)) {
        MODULE_DECL_CACHE.set(node, true);
        return true;
      }

      MODULE_DECL_CACHE.set(node, false);
      return false;
    }
```
</details>

- **Parameters**:
  - `node: ModuleDeclarationWithBody | TSESTree.Program`
- **Return Type**: `boolean`
- **Calls**:
  - `MODULE_DECL_CACHE.get`
  - `getStatementsOfNode`
  - `hasOverridingExportStatement`
  - `MODULE_DECL_CACHE.set`
### `ambientDeclarationSelector(parent: string): string`

<details><summary>Code</summary>

```ts
function ambientDeclarationSelector(parent: string): string {
      return [
        // Types are ambiently exported
        `${parent} > :matches(${[
          AST_NODE_TYPES.TSInterfaceDeclaration,
          AST_NODE_TYPES.TSTypeAliasDeclaration,
        ].join(', ')})`,
        // Value things are ambiently exported if they are "declare"d
        `${parent} > :matches(${[
          AST_NODE_TYPES.ClassDeclaration,
          AST_NODE_TYPES.TSDeclareFunction,
          AST_NODE_TYPES.TSEnumDeclaration,
          AST_NODE_TYPES.TSModuleDeclaration,
          AST_NODE_TYPES.VariableDeclaration,
        ].join(', ')})`,
      ].join(', ');
    }
```
</details>

- **Parameters**:
  - `parent: string`
- **Return Type**: `string`
- **Calls**:
  - `[
        // Types are ambiently exported
        `${parent} > :matches(${[
          AST_NODE_TYPES.TSInterfaceDeclaration,
          AST_NODE_TYPES.TSTypeAliasDeclaration,
        ].join(', ')})`,
        // Value things are ambiently exported if they are "declare"d
        `${parent} > :matches(${[
          AST_NODE_TYPES.ClassDeclaration,
          AST_NODE_TYPES.TSDeclareFunction,
          AST_NODE_TYPES.TSEnumDeclaration,
          AST_NODE_TYPES.TSModuleDeclaration,
          AST_NODE_TYPES.VariableDeclaration,
        ].join(', ')})`,
      ].join`
  - `[
          AST_NODE_TYPES.TSInterfaceDeclaration,
          AST_NODE_TYPES.TSTypeAliasDeclaration,
        ].join`
  - `[
          AST_NODE_TYPES.ClassDeclaration,
          AST_NODE_TYPES.TSDeclareFunction,
          AST_NODE_TYPES.TSEnumDeclaration,
          AST_NODE_TYPES.TSModuleDeclaration,
          AST_NODE_TYPES.VariableDeclaration,
        ].join`
- **Internal Comments**:
```
// Types are ambiently exported (x2)
// Value things are ambiently exported if they are "declare"d (x2)
```

### `markDeclarationChildAsUsed(node: DeclarationSelectorNode): void`

<details><summary>Code</summary>

```ts
function markDeclarationChildAsUsed(node: DeclarationSelectorNode): void {
      const identifiers: TSESTree.Identifier[] = [];
      switch (node.type) {
        case AST_NODE_TYPES.TSInterfaceDeclaration:
        case AST_NODE_TYPES.TSTypeAliasDeclaration:
        case AST_NODE_TYPES.ClassDeclaration:
        case AST_NODE_TYPES.FunctionDeclaration:
        case AST_NODE_TYPES.TSDeclareFunction:
        case AST_NODE_TYPES.TSEnumDeclaration:
        case AST_NODE_TYPES.TSModuleDeclaration:
          if (node.id?.type === AST_NODE_TYPES.Identifier) {
            identifiers.push(node.id);
          }
          break;

        case AST_NODE_TYPES.VariableDeclaration:
          for (const declaration of node.declarations) {
            visitPattern(declaration, pattern => {
              identifiers.push(pattern);
            });
          }
          break;
      }

      let scope = context.sourceCode.getScope(node);
      const shouldUseUpperScope = [
        AST_NODE_TYPES.TSDeclareFunction,
        AST_NODE_TYPES.TSModuleDeclaration,
      ].includes(node.type);

      if (scope.variableScope !== scope) {
        scope = scope.variableScope;
      } else if (shouldUseUpperScope && scope.upper) {
        scope = scope.upper;
      }

      for (const id of identifiers) {
        const superVar = scope.set.get(id.name);
        if (superVar) {
          superVar.eslintUsed = true;
        }
      }
    }
```
</details>

- **Parameters**:
  - `node: DeclarationSelectorNode`
- **Return Type**: `void`
- **Calls**:
  - `identifiers.push`
  - `visitPattern`
  - `context.sourceCode.getScope`
  - `[
        AST_NODE_TYPES.TSDeclareFunction,
        AST_NODE_TYPES.TSModuleDeclaration,
      ].includes`
  - `scope.set.get`
### `visitPattern(node: TSESTree.Node, cb: (node: TSESTree.Identifier) => void): void`

<details><summary>Code</summary>

```ts
function visitPattern(
      node: TSESTree.Node,
      cb: (node: TSESTree.Identifier) => void,
    ): void {
      const visitor = new PatternVisitor({}, node, cb);
      visitor.visit(node);
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `cb: (node: TSESTree.Identifier) => void`
- **Return Type**: `void`
- **Calls**:
  - `visitor.visit`
### `hasOverridingExportStatement(body: TSESTree.ProgramStatement[]): boolean`

<details><summary>Code</summary>

```ts
function hasOverridingExportStatement(
  body: TSESTree.ProgramStatement[],
): boolean {
  for (const statement of body) {
    if (
      (statement.type === AST_NODE_TYPES.ExportNamedDeclaration &&
        statement.declaration == null) ||
      statement.type === AST_NODE_TYPES.ExportAllDeclaration ||
      statement.type === AST_NODE_TYPES.TSExportAssignment
    ) {
      return true;
    }

    if (
      statement.type === AST_NODE_TYPES.ExportDefaultDeclaration &&
      statement.declaration.type === AST_NODE_TYPES.Identifier
    ) {
      return true;
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `body: TSESTree.ProgramStatement[]`
- **Return Type**: `boolean`
### `getStatementsOfNode(block: ModuleDeclarationWithBody | TSESTree.Program): TSESTree.ProgramStatement[]`

<details><summary>Code</summary>

```ts
function getStatementsOfNode(
  block: ModuleDeclarationWithBody | TSESTree.Program,
): TSESTree.ProgramStatement[] {
  if (block.type === AST_NODE_TYPES.Program) {
    return block.body;
  }

  return block.body.body;
}
```
</details>

- **Parameters**:
  - `block: ModuleDeclarationWithBody | TSESTree.Program`
- **Return Type**: `TSESTree.ProgramStatement[]`

---

## Interfaces

### `TranslatedOptions`

<details><summary>Interface Code</summary>

```ts
interface TranslatedOptions {
  args: 'after-used' | 'all' | 'none';
  argsIgnorePattern?: RegExp;
  caughtErrors: 'all' | 'none';
  caughtErrorsIgnorePattern?: RegExp;
  destructuredArrayIgnorePattern?: RegExp;
  ignoreClassWithStaticInitBlock: boolean;
  ignoreRestSiblings: boolean;
  reportUsedIgnorePattern: boolean;
  vars: 'all' | 'local';
  varsIgnorePattern?: RegExp;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `args` | `'after-used' | 'all' | 'none'` | ✗ |  |
| `argsIgnorePattern` | `RegExp` | ✓ |  |
| `caughtErrors` | `'all' | 'none'` | ✗ |  |
| `caughtErrorsIgnorePattern` | `RegExp` | ✓ |  |
| `destructuredArrayIgnorePattern` | `RegExp` | ✓ |  |
| `ignoreClassWithStaticInitBlock` | `boolean` | ✗ |  |
| `ignoreRestSiblings` | `boolean` | ✗ |  |
| `reportUsedIgnorePattern` | `boolean` | ✗ |  |
| `vars` | `'all' | 'local'` | ✗ |  |
| `varsIgnorePattern` | `RegExp` | ✓ |  |


---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = 'unusedVar' | 'usedIgnoredVar' | 'usedOnlyAsType';
```

### `Options`

```ts
type Options = [
  | 'all'
  | 'local'
  | {
      args?: 'after-used' | 'all' | 'none';
      argsIgnorePattern?: string;
      caughtErrors?: 'all' | 'none';
      caughtErrorsIgnorePattern?: string;
      destructuredArrayIgnorePattern?: string;
      ignoreClassWithStaticInitBlock?: boolean;
      ignoreRestSiblings?: boolean;
      reportUsedIgnorePattern?: boolean;
      vars?: 'all' | 'local';
      varsIgnorePattern?: string;
    },
];
```

### `VariableType`

```ts
type VariableType = | 'array-destructure'
  | 'catch-clause'
  | 'parameter'
  | 'variable';
```

### `ModuleDeclarationWithBody`

```ts
type ModuleDeclarationWithBody = MakeRequired<
  TSESTree.TSModuleDeclaration,
  'body'
>;
```

### `DeclarationSelectorNode`

```ts
type DeclarationSelectorNode = | TSESTree.ClassDeclaration
      | TSESTree.FunctionDeclaration
      | TSESTree.TSDeclareFunction
      | TSESTree.TSEnumDeclaration
      | TSESTree.TSInterfaceDeclaration
      | TSESTree.TSModuleDeclaration
      | TSESTree.TSTypeAliasDeclaration
      | TSESTree.VariableDeclaration;
```


---