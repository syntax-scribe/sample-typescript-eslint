[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `unified-signatures.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 32 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 32 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 9 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/unified-signatures.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `Equal` | `../util` |
| `arraysAreEqual` | `../util` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `overloads` | `string` | const | `otherLine == null
          ? 'These overloads'
          : `This overload and the one on line ${otherLine}`` | ✗ |
| `lineOfOtherOverload` | `any` | const | `only2 ? undefined : p0.loc.start.line` | ✗ |
| `typeAnnotation0` | `any` | const | `isTSParameterProperty(p0)
              ? p0.parameter.typeAnnotation
              : p0.typeAnnotation` | ✗ |
| `typeAnnotation1` | `any` | const | `isTSParameterProperty(p1)
              ? p1.parameter.typeAnnotation
              : p1.typeAnnotation` | ✗ |
| `lineOfOtherOverload` | `any` | const | `only2
              ? undefined
              : otherSignature.loc.start.line` | ✗ |
| `result` | `Failure[]` | const | `[]` | ✗ |
| `signature0` | `any` | const | `(a as Partial<MethodDefinition>).value ?? a` | ✗ |
| `signature1` | `any` | const | `(b as Partial<MethodDefinition>).value ?? b` | ✗ |
| `aTypeParams` | `any` | const | `a.typeParameters != null ? a.typeParameters.params : undefined` | ✗ |
| `bTypeParams` | `any` | const | `b.typeParameters != null ? b.typeParameters.params : undefined` | ✗ |
| `firstParam1` | `TSESTree.Parameter` | const | `types1[0]` | ✗ |
| `firstParam2` | `TSESTree.Parameter` | const | `types2[0]` | ✗ |
| `a` | `TSESTree.Parameter` | const | `types1[index]` | ✗ |
| `b` | `TSESTree.Parameter` | const | `types2[index]` | ✗ |
| `sig1` | `any` | const | `a.params` | ✗ |
| `sig2` | `any` | const | `b.params` | ✗ |
| `longer` | `any` | const | `sig1.length < sig2.length ? sig2 : sig1` | ✗ |
| `shorter` | `any` | const | `sig1.length < sig2.length ? sig1 : sig2` | ✗ |
| `shorterSig` | `any` | const | `sig1.length < sig2.length ? a : b` | ✗ |
| `sig1i` | `any` | const | `sig1[i]` | ✗ |
| `sig2i` | `any` | const | `sig2[i]` | ✗ |
| `typeAnnotation1` | `any` | const | `isTSParameterProperty(sig1i)
          ? sig1i.parameter.typeAnnotation
          : sig1i.typeAnnotation` | ✗ |
| `typeAnnotation2` | `any` | const | `isTSParameterProperty(sig2i)
          ? sig2i.parameter.typeAnnotation
          : sig2i.typeAnnotation` | ✗ |
| `set` | `Set<string>` | const | `new Set<string>()` | ✗ |
| `typeName` | `any` | const | `type.typeName` | ✗ |
| `typeAnnotationA` | `any` | const | `isTSParameterProperty(a)
        ? a.parameter.typeAnnotation
        : a.typeAnnotation` | ✗ |
| `typeAnnotationB` | `any` | const | `isTSParameterProperty(b)
        ? b.parameter.typeAnnotation
        : b.typeAnnotation` | ✗ |
| `optional` | `any` | const | `isTSParameterProperty(p)
        ? p.parameter.optional
        : p.optional` | ✗ |
| `optionalA` | `any` | const | `isTSParameterProperty(a)
        ? a.parameter.optional
        : a.optional` | ✗ |
| `optionalB` | `any` | const | `isTSParameterProperty(b)
        ? b.parameter.optional
        : b.optional` | ✗ |
| `scopes` | `Scope[]` | const | `[]` | ✗ |
| `currentScope` | `Scope | undefined` | let/var | `{
      overloads: new Map<string, OverloadNode[]>(),
    }` | ✗ |


---

## Functions

### `failureStringStart(otherLine: number): string`

<details><summary>Code</summary>

```ts
function failureStringStart(otherLine?: number): string {
      // For only 2 overloads we don't need to specify which is the other one.
      const overloads =
        otherLine == null
          ? 'These overloads'
          : `This overload and the one on line ${otherLine}`;
      return `${overloads} can be combined into one signature`;
    }
```
</details>

- **Parameters**:
  - `otherLine: number`
- **Return Type**: `string`
- **Internal Comments**:
```
// For only 2 overloads we don't need to specify which is the other one. (x2)
```

### `addFailures(failures: Failure[]): void`

<details><summary>Code</summary>

```ts
function addFailures(failures: Failure[]): void {
      for (const failure of failures) {
        const { only2, unify } = failure;
        switch (unify.kind) {
          case 'single-parameter-difference': {
            const { p0, p1 } = unify;
            const lineOfOtherOverload = only2 ? undefined : p0.loc.start.line;

            const typeAnnotation0 = isTSParameterProperty(p0)
              ? p0.parameter.typeAnnotation
              : p0.typeAnnotation;
            const typeAnnotation1 = isTSParameterProperty(p1)
              ? p1.parameter.typeAnnotation
              : p1.typeAnnotation;

            context.report({
              loc: p1.loc,
              node: p1,
              messageId: 'singleParameterDifference',
              data: {
                failureStringStart: failureStringStart(lineOfOtherOverload),
                type1: context.sourceCode.getText(
                  typeAnnotation0?.typeAnnotation,
                ),
                type2: context.sourceCode.getText(
                  typeAnnotation1?.typeAnnotation,
                ),
              },
            });
            break;
          }
          case 'extra-parameter': {
            const { extraParameter, otherSignature } = unify;
            const lineOfOtherOverload = only2
              ? undefined
              : otherSignature.loc.start.line;

            context.report({
              loc: extraParameter.loc,
              node: extraParameter,
              messageId:
                extraParameter.type === AST_NODE_TYPES.RestElement
                  ? 'omittingRestParameter'
                  : 'omittingSingleParameter',
              data: {
                failureStringStart: failureStringStart(lineOfOtherOverload),
              },
            });
          }
        }
      }
    }
```
</details>

- **Parameters**:
  - `failures: Failure[]`
- **Return Type**: `void`
- **Calls**:
  - `isTSParameterProperty`
  - `context.report`
  - `failureStringStart`
  - `context.sourceCode.getText`
### `checkOverloads(signatures: readonly OverloadNode[][], typeParameters: TSESTree.TSTypeParameterDeclaration): Failure[]`

<details><summary>Code</summary>

```ts
function checkOverloads(
      signatures: readonly OverloadNode[][],
      typeParameters?: TSESTree.TSTypeParameterDeclaration,
    ): Failure[] {
      const result: Failure[] = [];
      const isTypeParameter = getIsTypeParameter(typeParameters);
      for (const overloads of signatures) {
        forEachPair(overloads, (a, b) => {
          const signature0 = (a as Partial<MethodDefinition>).value ?? a;
          const signature1 = (b as Partial<MethodDefinition>).value ?? b;

          const unify = compareSignatures(
            signature0 as SignatureDefinition,
            signature1 as SignatureDefinition,
            isTypeParameter,
          );
          if (unify != null) {
            result.push({ only2: overloads.length === 2, unify });
          }
        });
      }
      return result;
    }
```
</details>

- **Parameters**:
  - `signatures: readonly OverloadNode[][]`
  - `typeParameters: TSESTree.TSTypeParameterDeclaration`
- **Return Type**: `Failure[]`
- **Calls**:
  - `getIsTypeParameter`
  - `forEachPair`
  - `compareSignatures`
  - `result.push`
### `compareSignatures(a: SignatureDefinition, b: SignatureDefinition, isTypeParameter: IsTypeParameter): Unify | undefined`

<details><summary>Code</summary>

```ts
function compareSignatures(
      a: SignatureDefinition,
      b: SignatureDefinition,
      isTypeParameter: IsTypeParameter,
    ): Unify | undefined {
      if (!signaturesCanBeUnified(a, b, isTypeParameter)) {
        return undefined;
      }

      return a.params.length === b.params.length
        ? signaturesDifferBySingleParameter(a.params, b.params)
        : signaturesDifferByOptionalOrRestParameter(a, b);
    }
```
</details>

- **Parameters**:
  - `a: SignatureDefinition`
  - `b: SignatureDefinition`
  - `isTypeParameter: IsTypeParameter`
- **Return Type**: `Unify | undefined`
- **Calls**:
  - `signaturesCanBeUnified`
  - `signaturesDifferBySingleParameter`
  - `signaturesDifferByOptionalOrRestParameter`
### `signaturesCanBeUnified(a: SignatureDefinition, b: SignatureDefinition, isTypeParameter: IsTypeParameter): boolean`

<details><summary>Code</summary>

```ts
function signaturesCanBeUnified(
      a: SignatureDefinition,
      b: SignatureDefinition,
      isTypeParameter: IsTypeParameter,
    ): boolean {
      // Must return the same type.

      const aTypeParams =
        a.typeParameters != null ? a.typeParameters.params : undefined;
      const bTypeParams =
        b.typeParameters != null ? b.typeParameters.params : undefined;

      if (ignoreDifferentlyNamedParameters) {
        const commonParamsLength = Math.min(a.params.length, b.params.length);
        for (let i = 0; i < commonParamsLength; i += 1) {
          if (
            a.params[i].type === b.params[i].type &&
            getStaticParameterName(a.params[i]) !==
              getStaticParameterName(b.params[i])
          ) {
            return false;
          }
        }
      }

      if (ignoreOverloadsWithDifferentJSDoc) {
        const aComment = getBlockCommentForNode(getExportingNode(a) ?? a);
        const bComment = getBlockCommentForNode(getExportingNode(b) ?? b);

        if (aComment?.value !== bComment?.value) {
          return false;
        }
      }

      return (
        typesAreEqual(a.returnType, b.returnType) &&
        // Must take the same type parameters.
        // If one uses a type parameter (from outside) and the other doesn't, they shouldn't be joined.
        arraysAreEqual(aTypeParams, bTypeParams, typeParametersAreEqual) &&
        signatureUsesTypeParameter(a, isTypeParameter) ===
          signatureUsesTypeParameter(b, isTypeParameter)
      );
    }
```
</details>

- **Parameters**:
  - `a: SignatureDefinition`
  - `b: SignatureDefinition`
  - `isTypeParameter: IsTypeParameter`
- **Return Type**: `boolean`
- **Calls**:
  - `Math.min`
  - `getStaticParameterName`
  - `getBlockCommentForNode`
  - `getExportingNode`
  - `typesAreEqual`
  - `arraysAreEqual (from ../util)`
  - `signatureUsesTypeParameter`
- **Internal Comments**:
```
// Must return the same type. (x2)
// Must take the same type parameters. (x2)
// If one uses a type parameter (from outside) and the other doesn't, they shouldn't be joined. (x2)
```

### `signaturesDifferBySingleParameter(types1: readonly TSESTree.Parameter[], types2: readonly TSESTree.Parameter[]): Unify | undefined`

<details><summary>Code</summary>

```ts
function signaturesDifferBySingleParameter(
      types1: readonly TSESTree.Parameter[],
      types2: readonly TSESTree.Parameter[],
    ): Unify | undefined {
      const firstParam1 = types1[0];
      const firstParam2 = types2[0];

      // exempt signatures with `this: void` from the rule
      if (isThisVoidParam(firstParam1) || isThisVoidParam(firstParam2)) {
        return undefined;
      }

      const index = getIndexOfFirstDifference(
        types1,
        types2,
        parametersAreEqual,
      );
      if (index == null) {
        return undefined;
      }

      // If remaining arrays are equal, the signatures differ by just one parameter type
      if (
        !arraysAreEqual(
          types1.slice(index + 1),
          types2.slice(index + 1),
          parametersAreEqual,
        )
      ) {
        return undefined;
      }

      const a = types1[index];
      const b = types2[index];
      // Can unify `a?: string` and `b?: number`. Can't unify `...args: string[]` and `...args: number[]`.
      // See https://github.com/Microsoft/TypeScript/issues/5077
      return parametersHaveEqualSigils(a, b) &&
        a.type !== AST_NODE_TYPES.RestElement
        ? { kind: 'single-parameter-difference', p0: a, p1: b }
        : undefined;
    }
```
</details>

- **JSDoc**:
```ts
/** Detect `a(x: number, y: number, z: number)` and `a(x: number, y: string, z: number)`. */
```

- **Parameters**:
  - `types1: readonly TSESTree.Parameter[]`
  - `types2: readonly TSESTree.Parameter[]`
- **Return Type**: `Unify | undefined`
- **Calls**:
  - `isThisVoidParam`
  - `getIndexOfFirstDifference`
  - `arraysAreEqual (from ../util)`
  - `types1.slice`
  - `types2.slice`
  - `parametersHaveEqualSigils`
- **Internal Comments**:
```
// exempt signatures with `this: void` from the rule
// If remaining arrays are equal, the signatures differ by just one parameter type
// Can unify `a?: string` and `b?: number`. Can't unify `...args: string[]` and `...args: number[]`.
// See https://github.com/Microsoft/TypeScript/issues/5077
```

### `isThisParam(param: TSESTree.Parameter | undefined): boolean`

<details><summary>Code</summary>

```ts
function isThisParam(param: TSESTree.Parameter | undefined): boolean {
      return (
        param != null &&
        param.type === AST_NODE_TYPES.Identifier &&
        param.name === 'this'
      );
    }
```
</details>

- **Parameters**:
  - `param: TSESTree.Parameter | undefined`
- **Return Type**: `boolean`
### `isThisVoidParam(param: TSESTree.Parameter | undefined): boolean`

<details><summary>Code</summary>

```ts
function isThisVoidParam(param: TSESTree.Parameter | undefined) {
      return (
        isThisParam(param) &&
        (param as TSESTree.Identifier).typeAnnotation?.typeAnnotation.type ===
          AST_NODE_TYPES.TSVoidKeyword
      );
    }
```
</details>

- **Parameters**:
  - `param: TSESTree.Parameter | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `isThisParam`
### `signaturesDifferByOptionalOrRestParameter(a: SignatureDefinition, b: SignatureDefinition): Unify | undefined`

<details><summary>Code</summary>

```ts
function signaturesDifferByOptionalOrRestParameter(
      a: SignatureDefinition,
      b: SignatureDefinition,
    ): Unify | undefined {
      const sig1 = a.params;
      const sig2 = b.params;

      const minLength = Math.min(sig1.length, sig2.length);
      const longer = sig1.length < sig2.length ? sig2 : sig1;
      const shorter = sig1.length < sig2.length ? sig1 : sig2;
      const shorterSig = sig1.length < sig2.length ? a : b;

      const firstParam1 = sig1.at(0);
      const firstParam2 = sig2.at(0);
      // If one signature has explicit this type and another doesn't, they can't
      // be unified.
      if (isThisParam(firstParam1) !== isThisParam(firstParam2)) {
        return undefined;
      }

      // exempt signatures with `this: void` from the rule
      if (isThisVoidParam(firstParam1) || isThisVoidParam(firstParam2)) {
        return undefined;
      }

      // If one is has 2+ parameters more than the other, they must all be optional/rest.
      // Differ by optional parameters: f() and f(x), f() and f(x, ?y, ...z)
      // Not allowed: f() and f(x, y)
      for (let i = minLength + 1; i < longer.length; i++) {
        if (!parameterMayBeMissing(longer[i])) {
          return undefined;
        }
      }

      for (let i = 0; i < minLength; i++) {
        const sig1i = sig1[i];
        const sig2i = sig2[i];
        const typeAnnotation1 = isTSParameterProperty(sig1i)
          ? sig1i.parameter.typeAnnotation
          : sig1i.typeAnnotation;
        const typeAnnotation2 = isTSParameterProperty(sig2i)
          ? sig2i.parameter.typeAnnotation
          : sig2i.typeAnnotation;

        if (!typesAreEqual(typeAnnotation1, typeAnnotation2)) {
          return undefined;
        }
      }

      if (
        minLength > 0 &&
        shorter[minLength - 1].type === AST_NODE_TYPES.RestElement
      ) {
        return undefined;
      }

      return {
        extraParameter: longer[longer.length - 1],
        kind: 'extra-parameter',
        otherSignature: shorterSig,
      };
    }
```
</details>

- **JSDoc**:
```ts
/**
     * Detect `a(): void` and `a(x: number): void`.
     * Returns the parameter declaration (`x: number` in this example) that should be optional/rest, and overload it's a part of.
     */
```

- **Parameters**:
  - `a: SignatureDefinition`
  - `b: SignatureDefinition`
- **Return Type**: `Unify | undefined`
- **Calls**:
  - `Math.min`
  - `sig1.at`
  - `sig2.at`
  - `isThisParam`
  - `isThisVoidParam`
  - `parameterMayBeMissing`
  - `isTSParameterProperty`
  - `typesAreEqual`
- **Internal Comments**:
```
// If one signature has explicit this type and another doesn't, they can't
// be unified.
// exempt signatures with `this: void` from the rule
// If one is has 2+ parameters more than the other, they must all be optional/rest.
// Differ by optional parameters: f() and f(x), f() and f(x, ?y, ...z)
// Not allowed: f() and f(x, y)
```

### `getIsTypeParameter(typeParameters: TSESTree.TSTypeParameterDeclaration): IsTypeParameter`

<details><summary>Code</summary>

```ts
function getIsTypeParameter(
      typeParameters?: TSESTree.TSTypeParameterDeclaration,
    ): IsTypeParameter {
      if (typeParameters == null) {
        return (() => false) as IsTypeParameter;
      }

      const set = new Set<string>();
      for (const t of typeParameters.params) {
        set.add(t.name.name);
      }
      return (typeName => set.has(typeName)) as IsTypeParameter;
    }
```
</details>

- **JSDoc**:
```ts
/** Given type parameters, returns a function to test whether a type is one of those parameters. */
```

- **Parameters**:
  - `typeParameters: TSESTree.TSTypeParameterDeclaration`
- **Return Type**: `IsTypeParameter`
- **Calls**:
  - `set.add`
  - `set.has`
### `signatureUsesTypeParameter(sig: SignatureDefinition, isTypeParameter: IsTypeParameter): boolean`

<details><summary>Code</summary>

```ts
function signatureUsesTypeParameter(
      sig: SignatureDefinition,
      isTypeParameter: IsTypeParameter,
    ): boolean {
      return sig.params.some((p: TSESTree.Parameter) =>
        typeContainsTypeParameter(
          isTSParameterProperty(p)
            ? p.parameter.typeAnnotation
            : p.typeAnnotation,
        ),
      );

      function typeContainsTypeParameter(
        type?: TSESTree.TSTypeAnnotation | TSESTree.TypeNode,
      ): boolean {
        if (!type) {
          return false;
        }

        if (type.type === AST_NODE_TYPES.TSTypeReference) {
          const typeName = type.typeName;
          if (isIdentifier(typeName) && isTypeParameter(typeName.name)) {
            return true;
          }
        }

        return typeContainsTypeParameter(
          (type as Partial<TSESTree.TSTypeAnnotation>).typeAnnotation ??
            (type as TSESTree.TSArrayType).elementType,
        );
      }
    }
```
</details>

- **JSDoc**:
```ts
/** True if any of the outer type parameters are used in a signature. */
```

- **Parameters**:
  - `sig: SignatureDefinition`
  - `isTypeParameter: IsTypeParameter`
- **Return Type**: `boolean`
- **Calls**:
  - `sig.params.some`
  - `typeContainsTypeParameter`
  - `isTSParameterProperty`
  - `isIdentifier`
  - `isTypeParameter`
### `typeContainsTypeParameter(type: TSESTree.TSTypeAnnotation | TSESTree.TypeNode): boolean`

<details><summary>Code</summary>

```ts
function typeContainsTypeParameter(
        type?: TSESTree.TSTypeAnnotation | TSESTree.TypeNode,
      ): boolean {
        if (!type) {
          return false;
        }

        if (type.type === AST_NODE_TYPES.TSTypeReference) {
          const typeName = type.typeName;
          if (isIdentifier(typeName) && isTypeParameter(typeName.name)) {
            return true;
          }
        }

        return typeContainsTypeParameter(
          (type as Partial<TSESTree.TSTypeAnnotation>).typeAnnotation ??
            (type as TSESTree.TSArrayType).elementType,
        );
      }
```
</details>

- **Parameters**:
  - `type: TSESTree.TSTypeAnnotation | TSESTree.TypeNode`
- **Return Type**: `boolean`
- **Calls**:
  - `isIdentifier`
  - `isTypeParameter`
  - `typeContainsTypeParameter`
### `isTSParameterProperty(node: TSESTree.Node): node is TSESTree.TSParameterProperty`

<details><summary>Code</summary>

```ts
function isTSParameterProperty(
      node: TSESTree.Node,
    ): node is TSESTree.TSParameterProperty {
      return node.type === AST_NODE_TYPES.TSParameterProperty;
    }
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.TSParameterProperty`
### `parametersAreEqual(a: TSESTree.Parameter, b: TSESTree.Parameter): boolean`

<details><summary>Code</summary>

```ts
function parametersAreEqual(
      a: TSESTree.Parameter,
      b: TSESTree.Parameter,
    ): boolean {
      const typeAnnotationA = isTSParameterProperty(a)
        ? a.parameter.typeAnnotation
        : a.typeAnnotation;
      const typeAnnotationB = isTSParameterProperty(b)
        ? b.parameter.typeAnnotation
        : b.typeAnnotation;

      return (
        parametersHaveEqualSigils(a, b) &&
        typesAreEqual(typeAnnotationA, typeAnnotationB)
      );
    }
```
</details>

- **Parameters**:
  - `a: TSESTree.Parameter`
  - `b: TSESTree.Parameter`
- **Return Type**: `boolean`
- **Calls**:
  - `isTSParameterProperty`
  - `parametersHaveEqualSigils`
  - `typesAreEqual`
### `parameterMayBeMissing(p: TSESTree.Parameter): boolean | undefined`

<details><summary>Code</summary>

```ts
function parameterMayBeMissing(p: TSESTree.Parameter): boolean | undefined {
      const optional = isTSParameterProperty(p)
        ? p.parameter.optional
        : p.optional;

      return p.type === AST_NODE_TYPES.RestElement || optional;
    }
```
</details>

- **JSDoc**:
```ts
/** True for optional/rest parameters. */
```

- **Parameters**:
  - `p: TSESTree.Parameter`
- **Return Type**: `boolean | undefined`
- **Calls**:
  - `isTSParameterProperty`
### `parametersHaveEqualSigils(a: TSESTree.Parameter, b: TSESTree.Parameter): boolean`

<details><summary>Code</summary>

```ts
function parametersHaveEqualSigils(
      a: TSESTree.Parameter,
      b: TSESTree.Parameter,
    ): boolean {
      const optionalA = isTSParameterProperty(a)
        ? a.parameter.optional
        : a.optional;
      const optionalB = isTSParameterProperty(b)
        ? b.parameter.optional
        : b.optional;

      return (
        (a.type === AST_NODE_TYPES.RestElement) ===
          (b.type === AST_NODE_TYPES.RestElement) && optionalA === optionalB
      );
    }
```
</details>

- **JSDoc**:
```ts
/** False if one is optional and the other isn't, or one is a rest parameter and the other isn't. */
```

- **Parameters**:
  - `a: TSESTree.Parameter`
  - `b: TSESTree.Parameter`
- **Return Type**: `boolean`
- **Calls**:
  - `isTSParameterProperty`
### `typeParametersAreEqual(a: TSESTree.TSTypeParameter, b: TSESTree.TSTypeParameter): boolean`

<details><summary>Code</summary>

```ts
function typeParametersAreEqual(
      a: TSESTree.TSTypeParameter,
      b: TSESTree.TSTypeParameter,
    ): boolean {
      return (
        a.name.name === b.name.name &&
        constraintsAreEqual(a.constraint, b.constraint)
      );
    }
```
</details>

- **Parameters**:
  - `a: TSESTree.TSTypeParameter`
  - `b: TSESTree.TSTypeParameter`
- **Return Type**: `boolean`
- **Calls**:
  - `constraintsAreEqual`
### `typesAreEqual(a: TSESTree.TSTypeAnnotation | undefined, b: TSESTree.TSTypeAnnotation | undefined): boolean`

<details><summary>Code</summary>

```ts
function typesAreEqual(
      a: TSESTree.TSTypeAnnotation | undefined,
      b: TSESTree.TSTypeAnnotation | undefined,
    ): boolean {
      return (
        a === b ||
        (a != null &&
          b != null &&
          context.sourceCode.getText(a.typeAnnotation) ===
            context.sourceCode.getText(b.typeAnnotation))
      );
    }
```
</details>

- **Parameters**:
  - `a: TSESTree.TSTypeAnnotation | undefined`
  - `b: TSESTree.TSTypeAnnotation | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `context.sourceCode.getText`
### `constraintsAreEqual(a: TSESTree.TypeNode | undefined, b: TSESTree.TypeNode | undefined): boolean`

<details><summary>Code</summary>

```ts
function constraintsAreEqual(
      a: TSESTree.TypeNode | undefined,
      b: TSESTree.TypeNode | undefined,
    ): boolean {
      return a === b || (a != null && b != null && a.type === b.type);
    }
```
</details>

- **Parameters**:
  - `a: TSESTree.TypeNode | undefined`
  - `b: TSESTree.TypeNode | undefined`
- **Return Type**: `boolean`
### `getIndexOfFirstDifference(a: readonly T[], b: readonly T[], equal: Equal<T>): number | undefined`

<details><summary>Code</summary>

```ts
function getIndexOfFirstDifference<T>(
      a: readonly T[],
      b: readonly T[],
      equal: Equal<T>,
    ): number | undefined {
      for (let i = 0; i < a.length && i < b.length; i++) {
        if (!equal(a[i], b[i])) {
          return i;
        }
      }
      return undefined;
    }
```
</details>

- **Parameters**:
  - `a: readonly T[]`
  - `b: readonly T[]`
  - `equal: Equal<T>`
- **Return Type**: `number | undefined`
- **Calls**:
  - `equal`
### `forEachPair(values: readonly T[], action: (a: T, b: T) => void): void`

<details><summary>Code</summary>

```ts
function forEachPair<T>(
      values: readonly T[],
      action: (a: T, b: T) => void,
    ): void {
      for (let i = 0; i < values.length; i++) {
        for (let j = i + 1; j < values.length; j++) {
          action(values[i], values[j]);
        }
      }
    }
```
</details>

- **JSDoc**:
```ts
/** Calls `action` for every pair of values in `values`. */
```

- **Parameters**:
  - `values: readonly T[]`
  - `action: (a: T, b: T) => void`
- **Return Type**: `void`
- **Calls**:
  - `action`
### `createScope(parent: ScopeNode, typeParameters: TSESTree.TSTypeParameterDeclaration): void`

<details><summary>Code</summary>

```ts
function createScope(
      parent: ScopeNode,
      typeParameters?: TSESTree.TSTypeParameterDeclaration,
    ): void {
      if (currentScope) {
        scopes.push(currentScope);
      }
      currentScope = {
        overloads: new Map<string, OverloadNode[]>(),
        parent,
        typeParameters,
      };
    }
```
</details>

- **Parameters**:
  - `parent: ScopeNode`
  - `typeParameters: TSESTree.TSTypeParameterDeclaration`
- **Return Type**: `void`
- **Calls**:
  - `scopes.push`
### `checkScope(): void`

<details><summary>Code</summary>

```ts
function checkScope(): void {
      const scope = nullThrows(
        currentScope,
        'checkScope() called without a current scope',
      );
      const failures = checkOverloads(
        [...scope.overloads.values()],
        scope.typeParameters,
      );
      addFailures(failures);
      currentScope = scopes.pop();
    }
```
</details>

- **Return Type**: `void`
- **Calls**:
  - `nullThrows (from ../util)`
  - `checkOverloads`
  - `scope.overloads.values`
  - `addFailures`
  - `scopes.pop`
### `getBlockCommentForNode(node: TSESTree.Node): TSESTree.Comment | undefined`

<details><summary>Code</summary>

```ts
function getBlockCommentForNode(
      node: TSESTree.Node,
    ): TSESTree.Comment | undefined {
      return context.sourceCode
        .getCommentsBefore(node)
        .reverse()
        .find(comment => comment.type === AST_TOKEN_TYPES.Block);
    }
```
</details>

- **JSDoc**:
```ts
/**
     * @returns the first valid JSDoc comment annotating `node`
     */
```

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `TSESTree.Comment | undefined`
- **Calls**:
  - `context.sourceCode
        .getCommentsBefore(node)
        .reverse()
        .find`
### `addOverload(signature: OverloadNode, key: string, containingNode: ContainingNode): void`

<details><summary>Code</summary>

```ts
function addOverload(
      signature: OverloadNode,
      key?: string,
      containingNode?: ContainingNode,
    ): void {
      key ??= getOverloadKey(signature);
      if (
        currentScope &&
        (containingNode ?? signature).parent === currentScope.parent
      ) {
        const overloads = currentScope.overloads.get(key);
        if (overloads != null) {
          overloads.push(signature);
        } else {
          currentScope.overloads.set(key, [signature]);
        }
      }
    }
```
</details>

- **Parameters**:
  - `signature: OverloadNode`
  - `key: string`
  - `containingNode: ContainingNode`
- **Return Type**: `void`
- **Calls**:
  - `getOverloadKey`
  - `currentScope.overloads.get`
  - `overloads.push`
  - `currentScope.overloads.set`
### `getExportingNode(node: SignatureDefinition): | TSESTree.ExportDefaultDeclaration
  | TSESTree.ExportNamedDeclaration
  | undefined`

<details><summary>Code</summary>

```ts
function getExportingNode(
  node: SignatureDefinition,
):
  | TSESTree.ExportDefaultDeclaration
  | TSESTree.ExportNamedDeclaration
  | undefined {
  return node.parent.type === AST_NODE_TYPES.ExportNamedDeclaration ||
    node.parent.type === AST_NODE_TYPES.ExportDefaultDeclaration
    ? node.parent
    : undefined;
}
```
</details>

- **Parameters**:
  - `node: SignatureDefinition`
- **Return Type**: `| TSESTree.ExportDefaultDeclaration
  | TSESTree.ExportNamedDeclaration
  | undefined`
### `getOverloadKey(node: OverloadNode): string`

<details><summary>Code</summary>

```ts
function getOverloadKey(node: OverloadNode): string {
  const info = getOverloadInfo(node);

  return (
    ((node as MethodDefinition).computed ? '0' : '1') +
    ((node as MethodDefinition).static ? '0' : '1') +
    info
  );
}
```
</details>

- **Parameters**:
  - `node: OverloadNode`
- **Return Type**: `string`
- **Calls**:
  - `getOverloadInfo`
### `getOverloadInfo(node: OverloadNode): string`

<details><summary>Code</summary>

```ts
function getOverloadInfo(node: OverloadNode): string {
  switch (node.type) {
    case AST_NODE_TYPES.TSConstructSignatureDeclaration:
      return 'constructor';
    case AST_NODE_TYPES.TSCallSignatureDeclaration:
      return '()';
    default: {
      const { key } = node as MethodDefinition;

      if (isPrivateIdentifier(key)) {
        return `private_identifier_${key.name}`;
      }

      if (isIdentifier(key)) {
        return `identifier_${key.name}`;
      }

      return (key as TSESTree.Literal).raw;
    }
  }
}
```
</details>

- **Parameters**:
  - `node: OverloadNode`
- **Return Type**: `string`
- **Calls**:
  - `isPrivateIdentifier`
  - `isIdentifier`
### `getStaticParameterName(param: TSESTree.Node): string | undefined`

<details><summary>Code</summary>

```ts
function getStaticParameterName(param: TSESTree.Node): string | undefined {
  switch (param.type) {
    case AST_NODE_TYPES.Identifier:
      return param.name;
    case AST_NODE_TYPES.RestElement:
      return getStaticParameterName(param.argument);
    default:
      return undefined;
  }
}
```
</details>

- **Parameters**:
  - `param: TSESTree.Node`
- **Return Type**: `string | undefined`
- **Calls**:
  - `getStaticParameterName`
### `isIdentifier(node: TSESTree.Node): node is TSESTree.Identifier`

<details><summary>Code</summary>

```ts
function isIdentifier(node: TSESTree.Node): node is TSESTree.Identifier {
  return node.type === AST_NODE_TYPES.Identifier;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.Identifier`
### `isPrivateIdentifier(node: TSESTree.Node): node is TSESTree.PrivateIdentifier`

<details><summary>Code</summary>

```ts
function isPrivateIdentifier(
  node: TSESTree.Node,
): node is TSESTree.PrivateIdentifier {
  return node.type === AST_NODE_TYPES.PrivateIdentifier;
}
```
</details>

- **Parameters**:
  - `node: TSESTree.Node`
- **Return Type**: `node is TSESTree.PrivateIdentifier`
### `isGetterOrSetter(node: | TSESTree.MethodDefinition
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSMethodSignature): boolean`

<details><summary>Code</summary>

```ts
function isGetterOrSetter(
  node:
    | TSESTree.MethodDefinition
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSMethodSignature,
): boolean {
  return node.kind === 'get' || node.kind === 'set';
}
```
</details>

- **Parameters**:
  - `node: | TSESTree.MethodDefinition
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSMethodSignature`
- **Return Type**: `boolean`

---

## Interfaces

### `Failure`

<details><summary>Interface Code</summary>

```ts
interface Failure {
  only2: boolean;
  unify: Unify;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `only2` | `boolean` | ✗ |  |
| `unify` | `Unify` | ✗ |  |

### `Scope`

<details><summary>Interface Code</summary>

```ts
interface Scope {
      overloads: Map<string, OverloadNode[]>;
      parent?: ScopeNode;
      typeParameters?: TSESTree.TSTypeParameterDeclaration;
    }
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `overloads` | `Map<string, OverloadNode[]>` | ✗ |  |
| `parent` | `ScopeNode` | ✓ |  |
| `typeParameters` | `TSESTree.TSTypeParameterDeclaration` | ✓ |  |


---

## Type Aliases

### `Unify`

```ts
type Unify = | {
      extraParameter: TSESTree.Parameter;
      kind: 'extra-parameter';
      otherSignature: SignatureDefinition;
    }
  | {
      kind: 'single-parameter-difference';
      p0: TSESTree.Parameter;
      p1: TSESTree.Parameter;
    };
```

### `IsTypeParameter`

/**
 * Returns true if typeName is the name of an *outer* type parameter.
 * In: `interface I<T> { m<U>(x: U): T }`, only `T` is an outer type parameter.
 */

```ts
type IsTypeParameter = (typeName: string) => boolean;
```

### `ScopeNode`

```ts
type ScopeNode = | TSESTree.ClassBody
  | TSESTree.Program
  | TSESTree.TSInterfaceBody
  | TSESTree.TSModuleBlock
  | TSESTree.TSTypeLiteral;
```

### `OverloadNode`

```ts
type OverloadNode = MethodDefinition | SignatureDefinition;
```

### `ContainingNode`

```ts
type ContainingNode = | TSESTree.ExportDefaultDeclaration
  | TSESTree.ExportNamedDeclaration;
```

### `SignatureDefinition`

```ts
type SignatureDefinition = | TSESTree.FunctionExpression
  | TSESTree.TSCallSignatureDeclaration
  | TSESTree.TSConstructSignatureDeclaration
  | TSESTree.TSDeclareFunction
  | TSESTree.TSEmptyBodyFunctionExpression
  | TSESTree.TSMethodSignature;
```

### `MethodDefinition`

```ts
type MethodDefinition = | TSESTree.MethodDefinition
  | TSESTree.TSAbstractMethodDefinition;
```

### `MessageIds`

```ts
type MessageIds = | 'omittingRestParameter'
  | 'omittingSingleParameter'
  | 'singleParameterDifference';
```

### `Options`

```ts
type Options = [
  {
    ignoreDifferentlyNamedParameters?: boolean;
    ignoreOverloadsWithDifferentJSDoc?: boolean;
  },
];
```


---