[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-unnecessary-type-assertion.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 7 |
| 🧱 Classes | 0 |
| 📦 Imports | 15 |
| 📊 Variables & Constants | 7 |
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
📂 **`packages/eslint-plugin/src/rules/no-unnecessary-type-assertion.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Scope` | `@typescript-eslint/scope-manager` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ReportFixFunction` | `@typescript-eslint/utils/ts-eslint` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getContextualType` | `../util` |
| `getDeclaration` | `../util` |
| `getModifiers` | `../util` |
| `getParserServices` | `../util` |
| `isNullableType` | `../util` |
| `isTypeFlagSet` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `parentScope` | `Scope | null` | let/var | `declaratorScope` | ✗ |
| `maybeDeclarationNode` | `any` | const | `parent.parent!` | ✗ |
| `uncastPartsSet` | `Set<unknown>` | const | `new Set(uncastParts)` | ✗ |
| `wouldSameTypeBeInferred` | `boolean` | const | `castTypeIsLiteral
          ? isImplicitlyNarrowedLiteralDeclaration(node)
          : !typeAnnotationIsConstAssertion` | ✗ |
| `isValidUndefined` | `any` | const | `typeIncludesUndefined
              ? contextualTypeIncludesUndefined
              : true` | ✗ |
| `isValidNull` | `any` | const | `typeIncludesNull
              ? contextualTypeIncludesNull
              : true` | ✗ |
| `isValidVoid` | `any` | const | `typeIncludesVoid
              ? contextualTypeIncludesVoid
              : true` | ✗ |


---

## Functions

### `isPossiblyUsedBeforeAssigned(node: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isPossiblyUsedBeforeAssigned(node: TSESTree.Expression): boolean {
      const declaration = getDeclaration(services, node);
      if (!declaration) {
        // don't know what the declaration is for some reason, so just assume the worst
        return true;
      }

      if (
        // non-strict mode doesn't care about used before assigned errors
        tsutils.isStrictCompilerOptionEnabled(
          compilerOptions,
          'strictNullChecks',
        ) &&
        // ignore class properties as they are compile time guarded
        // also ignore function arguments as they can't be used before defined
        ts.isVariableDeclaration(declaration)
      ) {
        // For var declarations, we need to check whether the node
        // is actually in a descendant of its declaration or not. If not,
        // it may be used before defined.

        // eg
        // if (Math.random() < 0.5) {
        //     var x: number  = 2;
        // } else {
        //     x!.toFixed();
        // }
        if (
          ts.isVariableDeclarationList(declaration.parent) &&
          // var
          declaration.parent.flags === ts.NodeFlags.None &&
          // If they are not in the same file it will not exist.
          // This situation must not occur using before defined.
          services.tsNodeToESTreeNodeMap.has(declaration)
        ) {
          const declaratorNode: TSESTree.VariableDeclaration =
            services.tsNodeToESTreeNodeMap.get(declaration);
          const scope = context.sourceCode.getScope(node);
          const declaratorScope = context.sourceCode.getScope(declaratorNode);
          let parentScope: Scope | null = declaratorScope;
          while ((parentScope = parentScope.upper)) {
            if (parentScope === scope) {
              return true;
            }
          }
        }

        if (
          // is it `const x!: number`
          declaration.initializer == null &&
          declaration.exclamationToken == null &&
          declaration.type != null
        ) {
          // check if the defined variable type has changed since assignment
          const declarationType = checker.getTypeFromTypeNode(declaration.type);
          const type = getConstrainedTypeAtLocation(services, node);
          if (
            declarationType === type &&
            // `declare`s are never narrowed, so never skip them
            !(
              ts.isVariableDeclarationList(declaration.parent) &&
              ts.isVariableStatement(declaration.parent.parent) &&
              tsutils.includesModifier(
                getModifiers(declaration.parent.parent),
                ts.SyntaxKind.DeclareKeyword,
              )
            )
          ) {
            // possibly used before assigned, so just skip it
            // better to false negative and skip it, than false positive and fix to compile erroring code
            //
            // no better way to figure this out right now
            // https://github.com/Microsoft/TypeScript/issues/31124
            return true;
          }
        }
      }
      return false;
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Returns true if there's a chance the variable has been used before a value has been assigned to it
     */
```

- **Parameters**:
  - `node: TSESTree.Expression`
- **Return Type**: `boolean`
- **Calls**:
  - `getDeclaration (from ../util)`
  - `tsutils.isStrictCompilerOptionEnabled`
  - `ts.isVariableDeclaration`
  - `ts.isVariableDeclarationList`
  - `services.tsNodeToESTreeNodeMap.has`
  - `services.tsNodeToESTreeNodeMap.get`
  - `context.sourceCode.getScope`
  - `checker.getTypeFromTypeNode`
  - `getConstrainedTypeAtLocation (from ../util)`
  - `ts.isVariableStatement`
  - `tsutils.includesModifier`
  - `getModifiers (from ../util)`
- **Internal Comments**:
```
// don't know what the declaration is for some reason, so just assume the worst
// non-strict mode doesn't care about used before assigned errors (x4)
// ignore class properties as they are compile time guarded (x3)
// also ignore function arguments as they can't be used before defined (x3)
// For var declarations, we need to check whether the node
// is actually in a descendant of its declaration or not. If not,
// it may be used before defined.
// eg
// if (Math.random() < 0.5) {
//     var x: number  = 2;
// } else {
//     x!.toFixed();
// }
// var (x4)
// If they are not in the same file it will not exist. (x4)
// This situation must not occur using before defined. (x4)
// is it `const x!: number` (x5)
// check if the defined variable type has changed since assignment (x2)
// `declare`s are never narrowed, so never skip them
// possibly used before assigned, so just skip it
// better to false negative and skip it, than false positive and fix to compile erroring code
//
// no better way to figure this out right now
// https://github.com/Microsoft/TypeScript/issues/31124
```

### `isConstAssertion(node: TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function isConstAssertion(node: TSESTree.TypeNode): boolean {
      return (
        node.type === AST_NODE_TYPES.TSTypeReference &&
        node.typeName.type === AST_NODE_TYPES.Identifier &&
        node.typeName.name === 'const'
      );
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.TypeNode`
- **Return Type**: `boolean`
### `isTemplateLiteralWithExpressions(expression: TSESTree.Expression): boolean`

<details><summary>Code</summary>

```ts
function isTemplateLiteralWithExpressions(expression: TSESTree.Expression) {
      return (
        expression.type === AST_NODE_TYPES.TemplateLiteral &&
        expression.expressions.length !== 0
      );
    }
```
</details>

- **Parameters**:
  - `expression: TSESTree.Expression`
- **Return Type**: `boolean`
### `isImplicitlyNarrowedLiteralDeclaration({
      expression,
      parent,
    }: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion): boolean`

<details><summary>Code</summary>

```ts
function isImplicitlyNarrowedLiteralDeclaration({
      expression,
      parent,
    }: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion): boolean {
      /**
       * Even on `const` variable declarations, template literals with expressions can sometimes be widened without a type assertion.
       * @see https://github.com/typescript-eslint/typescript-eslint/issues/8737
       */
      if (isTemplateLiteralWithExpressions(expression)) {
        return false;
      }

      // eslint-disable-next-line @typescript-eslint/no-non-null-assertion
      const maybeDeclarationNode = parent.parent!;

      return (
        (maybeDeclarationNode.type === AST_NODE_TYPES.VariableDeclaration &&
          maybeDeclarationNode.kind === 'const') ||
        (parent.type === AST_NODE_TYPES.PropertyDefinition && parent.readonly)
      );
    }
```
</details>

- **Parameters**:
  - `{
      expression,
      parent,
    }: TSESTree.TSAsExpression | TSESTree.TSTypeAssertion`
- **Return Type**: `boolean`
- **Calls**:
  - `isTemplateLiteralWithExpressions`
- **Internal Comments**:
```
/**
       * Even on `const` variable declarations, template literals with expressions can sometimes be widened without a type assertion.
       * @see https://github.com/typescript-eslint/typescript-eslint/issues/8737
       */
// eslint-disable-next-line @typescript-eslint/no-non-null-assertion (x2)
```

### `isTypeUnchanged(uncast: ts.Type, cast: ts.Type): boolean`

<details><summary>Code</summary>

```ts
function isTypeUnchanged(uncast: ts.Type, cast: ts.Type): boolean {
      if (uncast === cast) {
        return true;
      }

      if (
        isTypeFlagSet(uncast, ts.TypeFlags.Undefined) &&
        isTypeFlagSet(cast, ts.TypeFlags.Undefined) &&
        tsutils.isCompilerOptionEnabled(
          compilerOptions,
          'exactOptionalPropertyTypes',
        )
      ) {
        const uncastParts = tsutils
          .unionConstituents(uncast)
          .filter(part => !isTypeFlagSet(part, ts.TypeFlags.Undefined));

        const castParts = tsutils
          .unionConstituents(cast)
          .filter(part => !isTypeFlagSet(part, ts.TypeFlags.Undefined));

        if (uncastParts.length !== castParts.length) {
          return false;
        }

        const uncastPartsSet = new Set(uncastParts);
        return castParts.every(part => uncastPartsSet.has(part));
      }

      return false;
    }
```
</details>

- **Parameters**:
  - `uncast: ts.Type`
  - `cast: ts.Type`
- **Return Type**: `boolean`
- **Calls**:
  - `isTypeFlagSet (from ../util)`
  - `tsutils.isCompilerOptionEnabled`
  - `tsutils
          .unionConstituents(uncast)
          .filter`
  - `tsutils
          .unionConstituents(cast)
          .filter`
  - `castParts.every`
  - `uncastPartsSet.has`
### `isTypeLiteral(type: ts.Type): any`

<details><summary>Code</summary>

```ts
function isTypeLiteral(type: ts.Type) {
      return type.isLiteral() || tsutils.isBooleanLiteralType(type);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
- **Return Type**: `any`
- **Calls**:
  - `type.isLiteral`
  - `tsutils.isBooleanLiteralType`
### `removeExclamationFix(fixer: any): any`

<details><summary>Code</summary>

```ts
fixer => {
          const exclamationToken = nullThrows(
            context.sourceCode.getLastToken(node, token => token.value === '!'),
            NullThrowsReasons.MissingToken(
              'exclamation mark',
              'non-null assertion',
            ),
          );

          return fixer.removeRange(exclamationToken.range);
        }
```
</details>

- **Parameters**:
  - `fixer: any`
- **Return Type**: `any`
- **Calls**:
  - `nullThrows (from ../util)`
  - `context.sourceCode.getLastToken`
  - `NullThrowsReasons.MissingToken`
  - `fixer.removeRange`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    checkLiteralConstAssertions?: boolean;
    typesToIgnore?: string[];
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'contextuallyUnnecessary' | 'unnecessaryAssertion';
```


---