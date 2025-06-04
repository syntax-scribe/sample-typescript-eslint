[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `naming-convention.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 490 |
| 📦 Imports | 15 |
| 📊 Variables & Constants | 34 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/naming-convention.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `ScriptTarget` | `typescript` |
| `PatternVisitor` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TSESLint` | `@typescript-eslint/utils` |
| `Context` | `./naming-convention-utils` |
| `Selector` | `./naming-convention-utils` |
| `ValidatorFunction` | `./naming-convention-utils` |
| `_requiresQuoting` | `../util` |
| `collectVariables` | `../util` |
| `createRule` | `../util` |
| `getParserServices` | `../util` |
| `Modifiers` | `./naming-convention-utils` |
| `parseOptions` | `./naming-convention-utils` |
| `SCHEMA` | `./naming-convention-utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `defaultCamelCaseAllTheThingsConfig` | `Options` | const | `[
  {
    format: ['camelCase'],
    leadingUnderscore: 'allow',
    selector: 'default',
    trailingUnderscore: 'allow',
  },

  {
    format: ['camelCase', 'PascalCase'],
    selector: 'import',
  },

  {
    format: ['camelCase', 'UPPER_CASE'],
    leadingUnderscore: 'allow',
    selector: 'variable',
    trailingUnderscore: 'allow',
  },

  {
    format: ['PascalCase'],
    selector: 'typeLike',
  },
]` | ✗ |
| `context` | `any` | const | `contextWithoutDefaults.options.length > 0
        ? contextWithoutDefaults
        : // only apply the defaults when the user provides no config
          (Object.setPrototypeOf(
            {
              options: defaultCamelCaseAllTheThingsConfig,
            },
            contextWithoutDefaults,
          ) as Context)` | ✗ |
| `compilerOptions` | `any` | const | `getParserServices(context, true).program?.getCompilerOptions() ?? {}` | ✗ |
| `key` | `any` | const | `node.key` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `variable` | `TSESLint.Scope.Variable | null` | let/var | `null` | ✗ |
| `scope` | `TSESLint.Scope.Scope | null` | let/var | `initialScope` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `scope` | `any` | const | `context.sourceCode.getScope(node).upper` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `baseModifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `parent` | `any` | const | `node.parent` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set(baseModifiers)` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>([Modifiers.public])` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>([Modifiers.public])` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>([Modifiers.public])` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>([Modifiers.public])` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>([Modifiers.public])` | ✗ |
| `id` | `any` | const | `node.id` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `scope` | `any` | const | `context.sourceCode.getScope(node).upper` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `scope` | `any` | const | `context.sourceCode.getScope(node).upper` | ✗ |
| `id` | `any` | const | `node.id` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `modifiers` | `Set<Modifiers>` | const | `new Set<Modifiers>()` | ✗ |
| `selectors` | `{
      readonly [k in keyof TSESLint.RuleListener]: Readonly<{
        handler: (
          node: Parameters<NonNullable<TSESLint.RuleListener[k]>>[0],
          validator: ValidatorFunction,
        ) => void;
        validator: ValidatorFunction;
      }>;
    }` | const | `{
      // #region import

      'FunctionDeclaration, TSDeclareFunction, FunctionExpression': {
        handler: (
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        },
        validator: validators.function,
      },

      // #endregion

      // #region variable

      'ImportDefaultSpecifier, ImportNamespaceSpecifier, ImportSpecifier': {
        handler: (
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        },
        validator: validators.import,
      },

      // #endregion

      // #region function

      VariableDeclarator: {
        handler: (node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        },
        validator: validators.variable,
      },

      // #endregion function

      // #region parameter
      ':matches(PropertyDefinition, TSAbstractPropertyDefinition)[computed = false][value.type != "ArrowFunctionExpression"][value.type != "FunctionExpression"][value.type != "TSEmptyBodyFunctionExpression"]':
        {
          handler: (
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          },
          validator: validators.classProperty,
        },

      // #endregion parameter

      // #region parameterProperty

      ':not(ObjectPattern) > Property[computed = false][kind = "init"][value.type != "ArrowFunctionExpression"][value.type != "FunctionExpression"][value.type != "TSEmptyBodyFunctionExpression"]':
        {
          handler: (
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          },
          validator: validators.objectLiteralProperty,
        },

      // #endregion parameterProperty

      // #region property

      [[
        ':matches(PropertyDefinition, TSAbstractPropertyDefinition)[computed = false][value.type = "ArrowFunctionExpression"]',
        ':matches(PropertyDefinition, TSAbstractPropertyDefinition)[computed = false][value.type = "FunctionExpression"]',
        ':matches(PropertyDefinition, TSAbstractPropertyDefinition)[computed = false][value.type = "TSEmptyBodyFunctionExpression"]',
        ':matches(MethodDefinition, TSAbstractMethodDefinition)[computed = false][kind = "method"]',
      ].join(', ')]: {
        handler: (
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        },
        validator: validators.classMethod,
      },

      [[
        'MethodDefinition[computed = false]:matches([kind = "get"], [kind = "set"])',
        'TSAbstractMethodDefinition[computed = false]:matches([kind="get"], [kind="set"])',
      ].join(', ')]: {
        handler: (
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        },
        validator: validators.classicAccessor,
      },

      [[
        'Property[computed = false][kind = "init"][value.type = "ArrowFunctionExpression"]',
        'Property[computed = false][kind = "init"][value.type = "FunctionExpression"]',
        'Property[computed = false][kind = "init"][value.type = "TSEmptyBodyFunctionExpression"]',
      ].join(', ')]: {
        handler: (
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        },
        validator: validators.objectLiteralMethod,
      },

      // #endregion property

      // #region method

      [[
        'TSMethodSignature[computed = false]',
        'TSPropertySignature[computed = false][typeAnnotation.typeAnnotation.type = "TSFunctionType"]',
      ].join(', ')]: {
        handler: (
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        },
        validator: validators.typeMethod,
      },

      [[
        AST_NODE_TYPES.AccessorProperty,
        AST_NODE_TYPES.TSAbstractAccessorProperty,
      ].join(', ')]: {
        handler: (
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        },
        validator: validators.autoAccessor,
      },

      'FunctionDeclaration, TSDeclareFunction, TSEmptyBodyFunctionExpression, FunctionExpression, ArrowFunctionExpression':
        {
          handler: (
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          },
          validator: validators.parameter,
        },

      // #endregion method

      // #region accessor

      'Property[computed = false]:matches([kind = "get"], [kind = "set"])': {
        handler: (node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        },
        validator: validators.classicAccessor,
      },

      TSParameterProperty: {
        handler: (node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        },
        validator: validators.parameterProperty,
      },

      // #endregion accessor

      // #region autoAccessor

      'TSPropertySignature[computed = false][typeAnnotation.typeAnnotation.type != "TSFunctionType"]':
        {
          handler: (
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          },
          validator: validators.typeProperty,
        },

      // #endregion autoAccessor

      // #region enumMember

      // computed is optional, so can't do [computed = false]
      'ClassDeclaration, ClassExpression': {
        handler: (
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        },
        validator: validators.class,
      },

      // #endregion enumMember

      // #region class

      TSEnumDeclaration: {
        handler: (node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        },
        validator: validators.enum,
      },

      // #endregion class

      // #region interface

      'TSEnumMember[computed != true]': {
        handler: (
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        },
        validator: validators.enumMember,
      },

      // #endregion interface

      // #region typeAlias

      TSInterfaceDeclaration: {
        handler: (node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        },
        validator: validators.interface,
      },

      // #endregion typeAlias

      // #region enum

      TSTypeAliasDeclaration: {
        handler: (node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        },
        validator: validators.typeAlias,
      },

      // #endregion enum

      // #region typeParameter

      'TSTypeParameterDeclaration > TSTypeParameter': {
        handler: (node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        },
        validator: validators.typeParameter,
      },

      // #endregion typeParameter
    }` | ✗ |
| `identifiers` | `TSESTree.Identifier[]` | const | `[]` | ✗ |
| `visitor` | `any` | const | `new PatternVisitor({}, pattern, id => identifiers.push(id))` | ✗ |
| `refParent` | `any` | const | `ref.identifier.parent` | ✗ |
| `name` | `any` | const | `node.type === AST_NODE_TYPES.Identifier ||
    node.type === AST_NODE_TYPES.PrivateIdentifier
      ? node.name
      : `${node.value}`` | ✗ |


---

## Functions

### `handleMember(validator: ValidatorFunction, node: | TSESTree.AccessorPropertyNonComputedName
        | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName
        | TSESTree.TSPropertySignatureNonComputedName, modifiers: Set<Modifiers>): void`

<details><summary>Code</summary>

```ts
function handleMember(
      validator: ValidatorFunction,
      node:
        | TSESTree.AccessorPropertyNonComputedName
        | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName
        | TSESTree.TSPropertySignatureNonComputedName,
      modifiers: Set<Modifiers>,
    ): void {
      const key = node.key;
      if (requiresQuoting(key, compilerOptions.target)) {
        modifiers.add(Modifiers.requiresQuotes);
      }

      validator(key, modifiers);
    }
```
</details>

- **Parameters**:
  - `validator: ValidatorFunction`
  - `node: | TSESTree.AccessorPropertyNonComputedName
        | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName
        | TSESTree.TSPropertySignatureNonComputedName`
  - `modifiers: Set<Modifiers>`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `getMemberModifiers(node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty): Set<Modifiers>`

<details><summary>Code</summary>

```ts
function getMemberModifiers(
      node:
        | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty,
    ): Set<Modifiers> {
      const modifiers = new Set<Modifiers>();
      if ('key' in node && node.key.type === AST_NODE_TYPES.PrivateIdentifier) {
        modifiers.add(Modifiers['#private']);
      } else if (node.accessibility) {
        modifiers.add(Modifiers[node.accessibility]);
      } else {
        modifiers.add(Modifiers.public);
      }
      if (node.static) {
        modifiers.add(Modifiers.static);
      }
      if ('readonly' in node && node.readonly) {
        modifiers.add(Modifiers.readonly);
      }
      if ('override' in node && node.override) {
        modifiers.add(Modifiers.override);
      }
      if (
        node.type === AST_NODE_TYPES.TSAbstractPropertyDefinition ||
        node.type === AST_NODE_TYPES.TSAbstractMethodDefinition ||
        node.type === AST_NODE_TYPES.TSAbstractAccessorProperty
      ) {
        modifiers.add(Modifiers.abstract);
      }

      return modifiers;
    }
```
</details>

- **Parameters**:
  - `node: | TSESTree.AccessorProperty
        | TSESTree.MethodDefinition
        | TSESTree.PropertyDefinition
        | TSESTree.TSAbstractAccessorProperty
        | TSESTree.TSAbstractMethodDefinition
        | TSESTree.TSAbstractPropertyDefinition
        | TSESTree.TSParameterProperty`
- **Return Type**: `Set<Modifiers>`
- **Calls**:
  - `modifiers.add`
### `isUnused(name: string, initialScope: TSESLint.Scope.Scope | null): boolean`

<details><summary>Code</summary>

```ts
function isUnused(
      name: string,
      initialScope: TSESLint.Scope.Scope | null,
    ): boolean {
      let variable: TSESLint.Scope.Variable | null = null;
      let scope: TSESLint.Scope.Scope | null = initialScope;
      while (scope) {
        variable = scope.set.get(name) ?? null;
        if (variable) {
          break;
        }
        scope = scope.upper;
      }
      if (!variable) {
        return false;
      }

      return unusedVariables.has(variable);
    }
```
</details>

- **Parameters**:
  - `name: string`
  - `initialScope: TSESLint.Scope.Scope | null`
- **Return Type**: `boolean`
- **Calls**:
  - `scope.set.get`
  - `unusedVariables.has`
### `isDestructured(id: TSESTree.Identifier): boolean`

<details><summary>Code</summary>

```ts
function isDestructured(id: TSESTree.Identifier): boolean {
      return (
        // `const { x }`
        // does not match `const { x: y }`
        (id.parent.type === AST_NODE_TYPES.Property && id.parent.shorthand) ||
        // `const { x = 2 }`
        // does not match const `{ x: y = 2 }`
        (id.parent.type === AST_NODE_TYPES.AssignmentPattern &&
          id.parent.parent.type === AST_NODE_TYPES.Property &&
          id.parent.parent.shorthand)
      );
    }
```
</details>

- **Parameters**:
  - `id: TSESTree.Identifier`
- **Return Type**: `boolean`
- **Internal Comments**:
```
// `const { x }` (x2)
// does not match `const { x: y }` (x2)
// `const { x = 2 }`
// does not match const `{ x: y = 2 }`
```

### `isAsyncMemberOrProperty(propertyOrMemberNode: | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName): boolean`

<details><summary>Code</summary>

```ts
function isAsyncMemberOrProperty(
      propertyOrMemberNode:
        | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName,
    ): boolean {
      return Boolean(
        'value' in propertyOrMemberNode &&
          propertyOrMemberNode.value &&
          'async' in propertyOrMemberNode.value &&
          propertyOrMemberNode.value.async,
      );
    }
```
</details>

- **Parameters**:
  - `propertyOrMemberNode: | TSESTree.MethodDefinitionNonComputedName
        | TSESTree.PropertyDefinitionNonComputedName
        | TSESTree.PropertyNonComputedName
        | TSESTree.TSAbstractMethodDefinitionNonComputedName
        | TSESTree.TSAbstractPropertyDefinitionNonComputedName
        | TSESTree.TSMethodSignatureNonComputedName`
- **Return Type**: `boolean`
- **Calls**:
  - `Boolean`
### `isAsyncVariableIdentifier(id: TSESTree.Identifier): boolean`

<details><summary>Code</summary>

```ts
function isAsyncVariableIdentifier(id: TSESTree.Identifier): boolean {
      return Boolean(
        ('async' in id.parent && id.parent.async) ||
          ('init' in id.parent &&
            id.parent.init &&
            'async' in id.parent.init &&
            id.parent.init.async),
      );
    }
```
</details>

- **Parameters**:
  - `id: TSESTree.Identifier`
- **Return Type**: `boolean`
- **Calls**:
  - `Boolean`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction,
          validator,
        ): void => {
          if (node.id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // functions create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isGlobal(scope)) {
            modifiers.add(Modifiers.global);
          }

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          if (node.async) {
            modifiers.add(Modifiers.async);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.FunctionDeclaration
            | TSESTree.FunctionExpression
            | TSESTree.TSDeclareFunction`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isGlobal`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// functions create their own nested scope (x2)
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>();

          switch (node.type) {
            case AST_NODE_TYPES.ImportDefaultSpecifier:
              modifiers.add(Modifiers.default);
              break;
            case AST_NODE_TYPES.ImportNamespaceSpecifier:
              modifiers.add(Modifiers.namespace);
              break;
            case AST_NODE_TYPES.ImportSpecifier:
              // Handle `import { default as Foo }`
              if (
                node.imported.type === AST_NODE_TYPES.Identifier &&
                node.imported.name !== 'default'
              ) {
                return;
              }
              modifiers.add(Modifiers.default);
              break;
          }

          validator(node.local, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ImportDefaultSpecifier
            | TSESTree.ImportNamespaceSpecifier
            | TSESTree.ImportSpecifier`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `validator`
- **Internal Comments**:
```
// Handle `import { default as Foo }`
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const identifiers = getIdentifiersFromPattern(node.id);

          const baseModifiers = new Set<Modifiers>();
          const parent = node.parent;
          if (parent.kind === 'const') {
            baseModifiers.add(Modifiers.const);
          }

          if (isGlobal(context.sourceCode.getScope(node))) {
            baseModifiers.add(Modifiers.global);
          }

          identifiers.forEach(id => {
            const modifiers = new Set(baseModifiers);

            if (isDestructured(id)) {
              modifiers.add(Modifiers.destructured);
            }

            const scope = context.sourceCode.getScope(id);
            if (isExported(parent, id.name, scope)) {
              modifiers.add(Modifiers.exported);
            }

            if (isUnused(id.name, scope)) {
              modifiers.add(Modifiers.unused);
            }

            if (isAsyncVariableIdentifier(id)) {
              modifiers.add(Modifiers.async);
            }

            validator(id, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getIdentifiersFromPattern`
  - `baseModifiers.add`
  - `isGlobal`
  - `context.sourceCode.getScope`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `isAsyncVariableIdentifier`
  - `validator`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
            validator,
          ): void => {
            const modifiers = getMemberModifiers(node);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyDefinitionNonComputedName
              | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.PropertyNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinitionNonComputedName
            | TSESTree.PropertyDefinitionNonComputedName
            | TSESTree.TSAbstractMethodDefinitionNonComputedName
            | TSESTree.TSAbstractPropertyDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.MethodDefinitionNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.MethodDefinitionNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.MethodDefinitionNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);

          if (isAsyncMemberOrProperty(node)) {
            modifiers.add(Modifiers.async);
          }

          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.PropertyNonComputedName
            | TSESTree.TSMethodSignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `isAsyncMemberOrProperty`
  - `modifiers.add`
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node:
            | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName,
          validator,
        ): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: | TSESTree.TSMethodSignatureNonComputedName
            | TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: TSESTree.AccessorPropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.AccessorPropertyNonComputedName,
          validator,
        ): void => {
          const modifiers = getMemberModifiers(node);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.AccessorPropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `handleMember`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node:
              | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression,
            validator,
          ): void => {
            node.params.forEach(param => {
              if (param.type === AST_NODE_TYPES.TSParameterProperty) {
                return;
              }

              const identifiers = getIdentifiersFromPattern(param);

              identifiers.forEach(i => {
                const modifiers = new Set<Modifiers>();

                if (isDestructured(i)) {
                  modifiers.add(Modifiers.destructured);
                }

                if (isUnused(i.name, context.sourceCode.getScope(i))) {
                  modifiers.add(Modifiers.unused);
                }

                validator(i, modifiers);
              });
            });
          }
```
</details>

- **Parameters**:
  - `node: | TSESTree.ArrowFunctionExpression
              | TSESTree.FunctionDeclaration
              | TSESTree.FunctionExpression
              | TSESTree.TSDeclareFunction
              | TSESTree.TSEmptyBodyFunctionExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `node.params.forEach`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `isDestructured`
  - `modifiers.add`
  - `isUnused`
  - `context.sourceCode.getScope`
  - `validator`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: TSESTree.PropertyNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.PropertyNonComputedName, validator): void => {
          const modifiers = new Set<Modifiers>([Modifiers.public]);
          handleMember(validator, node, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.PropertyNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `handleMember`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = getMemberModifiers(node);

          const identifiers = getIdentifiersFromPattern(node.parameter);

          identifiers.forEach(i => {
            validator(i, modifiers);
          });
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `getMemberModifiers`
  - `getIdentifiersFromPattern`
  - `identifiers.forEach`
  - `validator`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.TSPropertySignatureNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
            node: TSESTree.TSPropertySignatureNonComputedName,
            validator,
          ): void => {
            const modifiers = new Set<Modifiers>([Modifiers.public]);
            if (node.readonly) {
              modifiers.add(Modifiers.readonly);
            }

            handleMember(validator, node, modifiers);
          }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSPropertySignatureNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `modifiers.add`
  - `handleMember`
### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: TSESTree.ClassDeclaration | TSESTree.ClassExpression, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.ClassDeclaration | TSESTree.ClassExpression,
          validator,
        ): void => {
          const id = node.id;
          if (id == null) {
            return;
          }

          const modifiers = new Set<Modifiers>();
          // classes create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (node.abstract) {
            modifiers.add(Modifiers.abstract);
          }

          if (isExported(node, id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.ClassDeclaration | TSESTree.ClassExpression`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `modifiers.add`
  - `isExported`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// classes create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          // enums create their own nested scope
          const scope = context.sourceCode.getScope(node).upper;

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
- **Internal Comments**:
```
// enums create their own nested scope (x2)
```

### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSEnumMemberNonComputedName, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(
          node: TSESTree.TSEnumMemberNonComputedName,
          validator,
        ): void => {
          const id = node.id;
          const modifiers = new Set<Modifiers>();

          if (requiresQuoting(id, compilerOptions.target)) {
            modifiers.add(Modifiers.requiresQuotes);
          }

          validator(id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSEnumMemberNonComputedName`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `requiresQuoting`
  - `modifiers.add`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: any, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isExported(node, node.id.name, scope)) {
            modifiers.add(Modifiers.exported);
          }

          if (isUnused(node.id.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.id, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: any`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isExported`
  - `modifiers.add`
  - `isUnused`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `handler(node: TSESTree.TSTypeParameter, validator: ValidatorFunction): void`

<details><summary>Code</summary>

```ts
(node: TSESTree.TSTypeParameter, validator): void => {
          const modifiers = new Set<Modifiers>();
          const scope = context.sourceCode.getScope(node);

          if (isUnused(node.name.name, scope)) {
            modifiers.add(Modifiers.unused);
          }

          validator(node.name, modifiers);
        }
```
</details>

- **Parameters**:
  - `node: TSESTree.TSTypeParameter`
  - `validator: ValidatorFunction`
- **Return Type**: `void`
- **Calls**:
  - `context.sourceCode.getScope`
  - `isUnused`
  - `modifiers.add`
  - `validator`
### `getIdentifiersFromPattern(pattern: TSESTree.DestructuringPattern): TSESTree.Identifier[]`

<details><summary>Code</summary>

```ts
function getIdentifiersFromPattern(
  pattern: TSESTree.DestructuringPattern,
): TSESTree.Identifier[] {
  const identifiers: TSESTree.Identifier[] = [];
  const visitor = new PatternVisitor({}, pattern, id => identifiers.push(id));
  visitor.visit(pattern);
  return identifiers;
}
```
</details>

- **Parameters**:
  - `pattern: TSESTree.DestructuringPattern`
- **Return Type**: `TSESTree.Identifier[]`
- **Calls**:
  - `identifiers.push`
  - `visitor.visit`
### `isExported(node: TSESTree.Node | undefined, name: string, scope: TSESLint.Scope.Scope | null): boolean`

<details><summary>Code</summary>

```ts
function isExported(
  node: TSESTree.Node | undefined,
  name: string,
  scope: TSESLint.Scope.Scope | null,
): boolean {
  if (
    node?.parent?.type === AST_NODE_TYPES.ExportDefaultDeclaration ||
    node?.parent?.type === AST_NODE_TYPES.ExportNamedDeclaration
  ) {
    return true;
  }

  if (scope == null) {
    return false;
  }

  const variable = scope.set.get(name);
  if (variable) {
    for (const ref of variable.references) {
      const refParent = ref.identifier.parent;
      if (
        refParent.type === AST_NODE_TYPES.ExportDefaultDeclaration ||
        refParent.type === AST_NODE_TYPES.ExportSpecifier
      ) {
        return true;
      }
    }
  }

  return false;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node | undefined`
  - `name: string`
  - `scope: TSESLint.Scope.Scope | null`
- **Return Type**: `boolean`
- **Calls**:
  - `scope.set.get`
### `isGlobal(scope: TSESLint.Scope.Scope | null): boolean`

<details><summary>Code</summary>

```ts
function isGlobal(scope: TSESLint.Scope.Scope | null): boolean {
  if (scope == null) {
    return false;
  }

  return (
    scope.type === TSESLint.Scope.ScopeType.global ||
    scope.type === TSESLint.Scope.ScopeType.module
  );
}
```
</details>

- **Parameters**:
  - `scope: TSESLint.Scope.Scope | null`
- **Return Type**: `boolean`
### `requiresQuoting(node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier, target: ScriptTarget | undefined): boolean`

<details><summary>Code</summary>

```ts
function requiresQuoting(
  node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier,
  target: ScriptTarget | undefined,
): boolean {
  const name =
    node.type === AST_NODE_TYPES.Identifier ||
    node.type === AST_NODE_TYPES.PrivateIdentifier
      ? node.name
      : `${node.value}`;
  return _requiresQuoting(name, target);
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Identifier | TSESTree.Literal | TSESTree.PrivateIdentifier`
  - `target: ScriptTarget | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `_requiresQuoting (from ../util)`

---

## Type Aliases

### `MessageIds`

```ts
type MessageIds = | 'doesNotMatchFormat'
  | 'doesNotMatchFormatTrimmed'
  | 'missingAffix'
  | 'missingUnderscore'
  | 'satisfyCustom'
  | 'unexpectedUnderscore';
```

### `Options`

```ts
type Options = Selector[];
```


---