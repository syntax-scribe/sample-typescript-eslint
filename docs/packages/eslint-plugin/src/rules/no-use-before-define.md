[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-use-before-define.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 15 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 11 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 1 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-use-before-define.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `TSESLint` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `referenceContainsTypeQuery` | `../util/referenceContainsTypeQuery` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `SENTINEL_TYPE` | `RegExp` | const | `/^(?:(?:Function|Class)(?:Declaration|Expression)|ArrowFunctionExpression|CatchClause|ImportDeclaration|ExportNamedDeclaration)$/` | ✗ |
| `functions` | `boolean` | let/var | `true` | ✗ |
| `classes` | `boolean` | let/var | `true` | ✗ |
| `enums` | `boolean` | let/var | `true` | ✗ |
| `variables` | `boolean` | let/var | `true` | ✗ |
| `typedefs` | `boolean` | let/var | `true` | ✗ |
| `ignoreTypeReferences` | `boolean` | let/var | `true` | ✗ |
| `allowNamedExports` | `boolean` | let/var | `false` | ✗ |
| `node` | `TSESTree.Node | undefined` | let/var | `variable.identifiers[0].parent` | ✗ |
| `location` | `any` | const | `reference.identifier.range[1]` | ✗ |
| `variable` | `any` | const | `reference.resolved` | ✗ |


---

## Functions

### `parseOptions(options: string | Config | null): Required<Config>`

<details><summary>Code</summary>

```ts
function parseOptions(options: string | Config | null): Required<Config> {
  let functions = true;
  let classes = true;
  let enums = true;
  let variables = true;
  let typedefs = true;
  let ignoreTypeReferences = true;
  let allowNamedExports = false;

  if (typeof options === 'string') {
    functions = options !== 'nofunc';
  } else if (typeof options === 'object' && options != null) {
    functions = options.functions !== false;
    classes = options.classes !== false;
    enums = options.enums !== false;
    variables = options.variables !== false;
    typedefs = options.typedefs !== false;
    ignoreTypeReferences = options.ignoreTypeReferences !== false;
    allowNamedExports = options.allowNamedExports !== false;
  }

  return {
    allowNamedExports,
    classes,
    enums,
    functions,
    ignoreTypeReferences,
    typedefs,
    variables,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Parses a given value as options.
 */
```

- **Parameters**:
  - `options: string | Config | null`
- **Return Type**: `Required<Config>`
### `isFunction(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isFunction(variable: TSESLint.Scope.Variable): boolean {
  return variable.defs[0].type === DefinitionType.FunctionName;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given variable is a function declaration.
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
### `isTypedef(variable: TSESLint.Scope.Variable): boolean`

<details><summary>Code</summary>

```ts
function isTypedef(variable: TSESLint.Scope.Variable): boolean {
  return variable.defs[0].type === DefinitionType.Type;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given variable is a type declaration.
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
- **Return Type**: `boolean`
### `isOuterEnum(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isOuterEnum(
  variable: TSESLint.Scope.Variable,
  reference: TSESLint.Scope.Reference,
): boolean {
  return (
    variable.defs[0].type === DefinitionType.TSEnumName &&
    variable.scope.variableScope !== reference.from.variableScope
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given variable is a enum declaration.
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
### `isOuterClass(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isOuterClass(
  variable: TSESLint.Scope.Variable,
  reference: TSESLint.Scope.Reference,
): boolean {
  return (
    variable.defs[0].type === DefinitionType.ClassName &&
    variable.scope.variableScope !== reference.from.variableScope
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given variable is a class declaration in an upper function scope.
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
### `isOuterVariable(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isOuterVariable(
  variable: TSESLint.Scope.Variable,
  reference: TSESLint.Scope.Reference,
): boolean {
  return (
    variable.defs[0].type === DefinitionType.Variable &&
    variable.scope.variableScope !== reference.from.variableScope
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given variable is a variable declaration in an upper function scope.
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
### `isNamedExports(reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isNamedExports(reference: TSESLint.Scope.Reference): boolean {
  const { identifier } = reference;
  return (
    identifier.parent.type === AST_NODE_TYPES.ExportSpecifier &&
    identifier.parent.local === identifier
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given reference is a export reference.
 */
```

- **Parameters**:
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
### `isTypeReference(reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isTypeReference(reference: TSESLint.Scope.Reference): boolean {
  return (
    reference.isTypeReference ||
    referenceContainsTypeQuery(reference.identifier)
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given reference is a type reference.
 */
```

- **Parameters**:
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `referenceContainsTypeQuery (from ../util/referenceContainsTypeQuery)`
### `isInRange(node: TSESTree.Expression | null | undefined, location: number): boolean`

<details><summary>Code</summary>

```ts
function isInRange(
  node: TSESTree.Expression | null | undefined,
  location: number,
): boolean {
  return !!node && node.range[0] <= location && location <= node.range[1];
}
```
</details>

- **JSDoc**:
```ts
/**
 * Checks whether or not a given location is inside of the range of a given node.
 */
```

- **Parameters**:
  - `node: TSESTree.Expression | null | undefined`
  - `location: number`
- **Return Type**: `boolean`
### `isClassRefInClassDecorator(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isClassRefInClassDecorator(
  variable: TSESLint.Scope.Variable,
  reference: TSESLint.Scope.Reference,
): boolean {
  if (
    variable.defs[0].type !== DefinitionType.ClassName ||
    variable.defs[0].node.decorators.length === 0
  ) {
    return false;
  }

  for (const deco of variable.defs[0].node.decorators) {
    if (
      reference.identifier.range[0] >= deco.range[0] &&
      reference.identifier.range[1] <= deco.range[1]
    ) {
      return true;
    }
  }

  return false;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Decorators are transpiled such that the decorator is placed after the class declaration
 * So it is considered safe
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
### `isInInitializer(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isInInitializer(
  variable: TSESLint.Scope.Variable,
  reference: TSESLint.Scope.Reference,
): boolean {
  if (variable.scope !== reference.from) {
    return false;
  }

  let node: TSESTree.Node | undefined = variable.identifiers[0].parent;
  const location = reference.identifier.range[1];

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
    } else if (SENTINEL_TYPE.test(node.type)) {
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
 * Checks whether or not a given reference is inside of the initializers of a given variable.
 *
 * @returns `true` in the following cases:
 * - var a = a
 * - var [a = a] = list
 * - var {a = a} = obj
 * - for (var a in a) {}
 * - for (var a of a) {}
 */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `isInRange`
  - `SENTINEL_TYPE.test`
### `isForbidden(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isForbidden(
      variable: TSESLint.Scope.Variable,
      reference: TSESLint.Scope.Reference,
    ): boolean {
      if (options.ignoreTypeReferences && isTypeReference(reference)) {
        return false;
      }
      if (isFunction(variable)) {
        return options.functions;
      }
      if (isOuterClass(variable, reference)) {
        return options.classes;
      }
      if (isOuterVariable(variable, reference)) {
        return options.variables;
      }
      if (isOuterEnum(variable, reference)) {
        return options.enums;
      }
      if (isTypedef(variable)) {
        return options.typedefs;
      }

      return true;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Determines whether a given use-before-define case should be reported according to the options.
     * @param variable The variable that gets used before being defined
     * @param reference The reference to the variable
     */
```

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeReference`
  - `isFunction`
  - `isOuterClass`
  - `isOuterVariable`
  - `isOuterEnum`
  - `isTypedef`
### `isDefinedBeforeUse(variable: TSESLint.Scope.Variable, reference: TSESLint.Scope.Reference): boolean`

<details><summary>Code</summary>

```ts
function isDefinedBeforeUse(
      variable: TSESLint.Scope.Variable,
      reference: TSESLint.Scope.Reference,
    ): boolean {
      return (
        variable.identifiers[0].range[1] <= reference.identifier.range[1] &&
        !(reference.isValueReference && isInInitializer(variable, reference))
      );
    }
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `reference: TSESLint.Scope.Reference`
- **Return Type**: `boolean`
- **Calls**:
  - `isInInitializer`
### `findVariablesInScope(scope: TSESLint.Scope.Scope): void`

<details><summary>Code</summary>

```ts
function findVariablesInScope(scope: TSESLint.Scope.Scope): void {
      scope.references.forEach(reference => {
        const variable = reference.resolved;

        function report(): void {
          context.report({
            node: reference.identifier,
            messageId: 'noUseBeforeDefine',
            data: {
              name: reference.identifier.name,
            },
          });
        }

        // Skips when the reference is:
        // - initializations.
        // - referring to an undefined variable.
        // - referring to a global environment variable (there're no identifiers).
        // - located preceded by the variable (except in initializers).
        // - allowed by options.
        if (reference.init) {
          return;
        }

        if (!options.allowNamedExports && isNamedExports(reference)) {
          if (!variable || !isDefinedBeforeUse(variable, reference)) {
            report();
          }
          return;
        }

        if (!variable) {
          return;
        }

        if (
          variable.identifiers.length === 0 ||
          isDefinedBeforeUse(variable, reference) ||
          !isForbidden(variable, reference) ||
          isClassRefInClassDecorator(variable, reference) ||
          reference.from.type === TSESLint.Scope.ScopeType.functionType
        ) {
          return;
        }

        // Reports.
        report();
      });

      scope.childScopes.forEach(findVariablesInScope);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Finds and validates all variables in a given scope.
     */
```

- **Parameters**:
  - `scope: TSESLint.Scope.Scope`
- **Return Type**: `void`
- **Calls**:
  - `scope.references.forEach`
  - `context.report`
  - `isNamedExports`
  - `isDefinedBeforeUse`
  - `report`
  - `isForbidden`
  - `isClassRefInClassDecorator`
  - `scope.childScopes.forEach`
- **Internal Comments**:
```
// Skips when the reference is:
// - initializations.
// - referring to an undefined variable.
// - referring to a global environment variable (there're no identifiers).
// - located preceded by the variable (except in initializers).
// - allowed by options.
// Reports. (x3)
```

### `report(): void`

<details><summary>Code</summary>

```ts
function report(): void {
          context.report({
            node: reference.identifier,
            messageId: 'noUseBeforeDefine',
            data: {
              name: reference.identifier.name,
            },
          });
        }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `context.report`

---

## Interfaces

### `Config`

<details><summary>Interface Code</summary>

```ts
export interface Config {
  allowNamedExports?: boolean;
  classes?: boolean;
  enums?: boolean;
  functions?: boolean;
  ignoreTypeReferences?: boolean;
  typedefs?: boolean;
  variables?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `allowNamedExports` | `boolean` | ✓ |  |
| `classes` | `boolean` | ✓ |  |
| `enums` | `boolean` | ✓ |  |
| `functions` | `boolean` | ✓ |  |
| `ignoreTypeReferences` | `boolean` | ✓ |  |
| `typedefs` | `boolean` | ✓ |  |
| `variables` | `boolean` | ✓ |  |


---

## Type Aliases

### `Options`

```ts
type Options = ['nofunc' | Config];
```

### `MessageIds`

```ts
type MessageIds = 'noUseBeforeDefine';
```


---