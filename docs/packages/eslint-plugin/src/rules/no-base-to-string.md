[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-base-to-string.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 9 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 6 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 1 |


## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)
- [Enums](#enums)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-base-to-string.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `getConstrainedTypeAtLocation` | `../util` |
| `getParserServices` | `../util` |
| `getTypeName` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ignoredTypeNames` | `any` | const | `option.ignoredTypeNames ?? []` | ✗ |
| `toString` | `any` | const | `checker.getPropertyOfType(type, 'toString') ??
        checker.getPropertyOfType(type, 'toLocaleString')` | ✗ |
| `declaration` | `any` | const | `declarations[0]` | ✗ |
| `isBaseToString` | `boolean` | const | `ts.isInterfaceDeclaration(declaration.parent) &&
        declaration.parent.name.text === 'Object'` | ✗ |
| `memberExpr` | `TSESTree.MemberExpression` | const | `node.parent as TSESTree.MemberExpression` | ✗ |
| `memberExpr` | `TSESTree.MemberExpression` | const | `node.parent as TSESTree.MemberExpression` | ✗ |


---

## Functions

### `checkExpression(node: TSESTree.Expression, type: ts.Type): void`

<details><summary>Code</summary>

```ts
function checkExpression(node: TSESTree.Expression, type?: ts.Type): void {
      if (node.type === AST_NODE_TYPES.Literal) {
        return;
      }
      const certainty = collectToStringCertainty(
        type ?? services.getTypeAtLocation(node),
        new Set(),
      );
      if (certainty === Usefulness.Always) {
        return;
      }

      context.report({
        node,
        messageId: 'baseToString',
        data: {
          name: context.sourceCode.getText(node),
          certainty,
        },
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Expression`
  - `type: ts.Type`
- **Return Type**: `void`
- **Calls**:
  - `collectToStringCertainty`
  - `services.getTypeAtLocation`
  - `context.report`
  - `context.sourceCode.getText`
### `checkExpressionForArrayJoin(node: TSESTree.Node, type: ts.Type): void`

<details><summary>Code</summary>

```ts
function checkExpressionForArrayJoin(
      node: TSESTree.Node,
      type: ts.Type,
    ): void {
      const certainty = collectJoinCertainty(type, new Set());

      if (certainty === Usefulness.Always) {
        return;
      }

      context.report({
        node,
        messageId: 'baseArrayJoin',
        data: {
          name: context.sourceCode.getText(node),
          certainty,
        },
      });
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
  - `type: ts.Type`
- **Return Type**: `void`
- **Calls**:
  - `collectJoinCertainty`
  - `context.report`
  - `context.sourceCode.getText`
### `collectUnionTypeCertainty(type: ts.UnionType, collectSubTypeCertainty: (type: ts.Type) => Usefulness): Usefulness`

<details><summary>Code</summary>

```ts
function collectUnionTypeCertainty(
      type: ts.UnionType,
      collectSubTypeCertainty: (type: ts.Type) => Usefulness,
    ): Usefulness {
      const certainties = type.types.map(t => collectSubTypeCertainty(t));
      if (certainties.every(certainty => certainty === Usefulness.Never)) {
        return Usefulness.Never;
      }

      if (certainties.every(certainty => certainty === Usefulness.Always)) {
        return Usefulness.Always;
      }

      return Usefulness.Sometimes;
    }
```
</details>

- **Parameters**:
  - `type: ts.UnionType`
  - `collectSubTypeCertainty: (type: ts.Type) => Usefulness`
- **Return Type**: `Usefulness`
- **Calls**:
  - `type.types.map`
  - `collectSubTypeCertainty`
  - `certainties.every`
### `collectIntersectionTypeCertainty(type: ts.IntersectionType, collectSubTypeCertainty: (type: ts.Type) => Usefulness): Usefulness`

<details><summary>Code</summary>

```ts
function collectIntersectionTypeCertainty(
      type: ts.IntersectionType,
      collectSubTypeCertainty: (type: ts.Type) => Usefulness,
    ): Usefulness {
      for (const subType of type.types) {
        const subtypeUsefulness = collectSubTypeCertainty(subType);

        if (subtypeUsefulness === Usefulness.Always) {
          return Usefulness.Always;
        }
      }

      return Usefulness.Never;
    }
```
</details>

- **Parameters**:
  - `type: ts.IntersectionType`
  - `collectSubTypeCertainty: (type: ts.Type) => Usefulness`
- **Return Type**: `Usefulness`
- **Calls**:
  - `collectSubTypeCertainty`
### `collectTupleCertainty(type: ts.TypeReference, visited: Set<ts.Type>): Usefulness`

<details><summary>Code</summary>

```ts
function collectTupleCertainty(
      type: ts.TypeReference,
      visited: Set<ts.Type>,
    ): Usefulness {
      const typeArgs = checker.getTypeArguments(type);
      const certainties = typeArgs.map(t =>
        collectToStringCertainty(t, visited),
      );
      if (certainties.some(certainty => certainty === Usefulness.Never)) {
        return Usefulness.Never;
      }

      if (certainties.some(certainty => certainty === Usefulness.Sometimes)) {
        return Usefulness.Sometimes;
      }

      return Usefulness.Always;
    }
```
</details>

- **Parameters**:
  - `type: ts.TypeReference`
  - `visited: Set<ts.Type>`
- **Return Type**: `Usefulness`
- **Calls**:
  - `checker.getTypeArguments`
  - `typeArgs.map`
  - `collectToStringCertainty`
  - `certainties.some`
### `collectArrayCertainty(type: ts.Type, visited: Set<ts.Type>): Usefulness`

<details><summary>Code</summary>

```ts
function collectArrayCertainty(
      type: ts.Type,
      visited: Set<ts.Type>,
    ): Usefulness {
      const elemType = nullThrows(
        type.getNumberIndexType(),
        'array should have number index type',
      );
      return collectToStringCertainty(elemType, visited);
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `visited: Set<ts.Type>`
- **Return Type**: `Usefulness`
- **Calls**:
  - `nullThrows (from ../util)`
  - `type.getNumberIndexType`
  - `collectToStringCertainty`
### `collectJoinCertainty(type: ts.Type, visited: Set<ts.Type>): Usefulness`

<details><summary>Code</summary>

```ts
function collectJoinCertainty(
      type: ts.Type,
      visited: Set<ts.Type>,
    ): Usefulness {
      if (tsutils.isUnionType(type)) {
        return collectUnionTypeCertainty(type, t =>
          collectJoinCertainty(t, visited),
        );
      }

      if (tsutils.isIntersectionType(type)) {
        return collectIntersectionTypeCertainty(type, t =>
          collectJoinCertainty(t, visited),
        );
      }

      if (checker.isTupleType(type)) {
        return collectTupleCertainty(type, visited);
      }

      if (checker.isArrayType(type)) {
        return collectArrayCertainty(type, visited);
      }

      return Usefulness.Always;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `visited: Set<ts.Type>`
- **Return Type**: `Usefulness`
- **Calls**:
  - `tsutils.isUnionType`
  - `collectUnionTypeCertainty`
  - `collectJoinCertainty`
  - `tsutils.isIntersectionType`
  - `collectIntersectionTypeCertainty`
  - `checker.isTupleType`
  - `collectTupleCertainty`
  - `checker.isArrayType`
  - `collectArrayCertainty`
### `collectToStringCertainty(type: ts.Type, visited: Set<ts.Type>): Usefulness`

<details><summary>Code</summary>

```ts
function collectToStringCertainty(
      type: ts.Type,
      visited: Set<ts.Type>,
    ): Usefulness {
      if (visited.has(type)) {
        // don't report if this is a self referencing array or tuple type
        return Usefulness.Always;
      }

      if (tsutils.isTypeParameter(type)) {
        const constraint = type.getConstraint();
        if (constraint) {
          return collectToStringCertainty(constraint, visited);
        }
        // unconstrained generic means `unknown`
        return Usefulness.Always;
      }

      // the Boolean type definition missing toString()
      if (
        type.flags & ts.TypeFlags.Boolean ||
        type.flags & ts.TypeFlags.BooleanLiteral
      ) {
        return Usefulness.Always;
      }

      if (ignoredTypeNames.includes(getTypeName(checker, type))) {
        return Usefulness.Always;
      }

      if (type.isIntersection()) {
        return collectIntersectionTypeCertainty(type, t =>
          collectToStringCertainty(t, visited),
        );
      }

      if (type.isUnion()) {
        return collectUnionTypeCertainty(type, t =>
          collectToStringCertainty(t, visited),
        );
      }

      if (checker.isTupleType(type)) {
        return collectTupleCertainty(type, new Set([...visited, type]));
      }

      if (checker.isArrayType(type)) {
        return collectArrayCertainty(type, new Set([...visited, type]));
      }

      const toString =
        checker.getPropertyOfType(type, 'toString') ??
        checker.getPropertyOfType(type, 'toLocaleString');
      if (!toString) {
        // e.g. any/unknown
        return Usefulness.Always;
      }

      const declarations = toString.getDeclarations();

      if (declarations == null || declarations.length !== 1) {
        // If there are multiple declarations, at least one of them must not be
        // the default object toString.
        //
        // This may only matter for older versions of TS
        // see https://github.com/typescript-eslint/typescript-eslint/issues/8585
        return Usefulness.Always;
      }

      const declaration = declarations[0];
      const isBaseToString =
        ts.isInterfaceDeclaration(declaration.parent) &&
        declaration.parent.name.text === 'Object';
      return isBaseToString ? Usefulness.Never : Usefulness.Always;
    }
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `visited: Set<ts.Type>`
- **Return Type**: `Usefulness`
- **Calls**:
  - `visited.has`
  - `tsutils.isTypeParameter`
  - `type.getConstraint`
  - `collectToStringCertainty`
  - `ignoredTypeNames.includes`
  - `getTypeName (from ../util)`
  - `type.isIntersection`
  - `collectIntersectionTypeCertainty`
  - `type.isUnion`
  - `collectUnionTypeCertainty`
  - `checker.isTupleType`
  - `collectTupleCertainty`
  - `checker.isArrayType`
  - `collectArrayCertainty`
  - `checker.getPropertyOfType`
  - `toString.getDeclarations`
  - `ts.isInterfaceDeclaration`
- **Internal Comments**:
```
// don't report if this is a self referencing array or tuple type
// unconstrained generic means `unknown`
// the Boolean type definition missing toString()
// e.g. any/unknown
// If there are multiple declarations, at least one of them must not be
// the default object toString.
//
// This may only matter for older versions of TS
// see https://github.com/typescript-eslint/typescript-eslint/issues/8585
```

### `isBuiltInStringCall(node: TSESTree.CallExpression): boolean`

<details><summary>Code</summary>

```ts
function isBuiltInStringCall(node: TSESTree.CallExpression): boolean {
      if (
        node.callee.type === AST_NODE_TYPES.Identifier &&
        // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
        node.callee.name === 'String' &&
        node.arguments[0]
      ) {
        const scope = context.sourceCode.getScope(node);
        // eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum
        const variable = scope.set.get('String');
        return !variable?.defs.length;
      }
      return false;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.CallExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getScope`
  - `scope.set.get`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/internal/prefer-ast-types-enum (x6)
```


---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    ignoredTypeNames?: string[];
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'baseArrayJoin' | 'baseToString';
```


---

## Enums

### `enum Usefulness`

<details><summary>Enum Code</summary>

```ts
enum Usefulness {
  Always = 'always',
  Never = 'will',
  Sometimes = 'may',
}
```
</details>

#### Members

| Name | Value | Description |
|------|-------|-------------|
| `Always` | `always` |  |
| `Never` | `will` |  |
| `Sometimes` | `may` |  |


---