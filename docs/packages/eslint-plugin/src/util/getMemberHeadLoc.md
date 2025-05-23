[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getMemberHeadLoc.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 4
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/getMemberHeadLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `nullThrows` | `@typescript-eslint/utils/eslint-utils` |
| `NullThrowsReasons` | `@typescript-eslint/utils/eslint-utils` |


---

## Functions

### `getMemberHeadLoc(sourceCode: Readonly<TSESLint.SourceCode>, node: | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getMemberHeadLoc(
  sourceCode: Readonly<TSESLint.SourceCode>,
  node:
    | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition,
): TSESTree.SourceLocation {
  let start: TSESTree.Position;

  if (node.decorators.length === 0) {
    start = node.loc.start;
  } else {
    const lastDecorator = node.decorators[node.decorators.length - 1];
    const nextToken = nullThrows(
      sourceCode.getTokenAfter(lastDecorator),
      NullThrowsReasons.MissingToken('token', 'last decorator'),
    );
    start = nextToken.loc.start;
  }

  let end: TSESTree.Position;

  if (!node.computed) {
    end = node.key.loc.end;
  } else {
    const closingBracket = nullThrows(
      sourceCode.getTokenAfter(node.key, token => token.value === ']'),
      NullThrowsReasons.MissingToken(']', node.type),
    );
    end = closingBracket.loc.end;
  }

  return {
    end: structuredClone(end),
    start: structuredClone(start),
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Generates report loc suitable for reporting on how a class member is
 * declared, rather than how it's implemented.
 *
 * ```ts
 * class A {
 *   abstract method(): void;
 *   ~~~~~~~~~~~~~~~
 *
 *   concreteMethod(): void {
 *   ~~~~~~~~~~~~~~
 *      // code
 *   }
 *
 *   abstract private property?: string;
 *   ~~~~~~~~~~~~~~~~~~~~~~~~~
 *
 *   @decorator override concreteProperty = 'value';
 *              ~~~~~~~~~~~~~~~~~~~~~~~~~
 * }
 * ```
 */
```

- **Parameters**:
  - `sourceCode: Readonly<TSESLint.SourceCode>`
  - `node: | TSESTree.AccessorProperty
    | TSESTree.MethodDefinition
    | TSESTree.PropertyDefinition
    | TSESTree.TSAbstractAccessorProperty
    | TSESTree.TSAbstractMethodDefinition
    | TSESTree.TSAbstractPropertyDefinition`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `nullThrows (from @typescript-eslint/utils/eslint-utils)`
  - `sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `structuredClone`
### `getParameterPropertyHeadLoc(sourceCode: Readonly<TSESLint.SourceCode>, node: TSESTree.TSParameterProperty, nodeName: string): TSESTree.SourceLocation`

<details><summary>Code</summary>

```ts
export function getParameterPropertyHeadLoc(
  sourceCode: Readonly<TSESLint.SourceCode>,
  node: TSESTree.TSParameterProperty,
  nodeName: string,
): TSESTree.SourceLocation {
  // Parameter properties have a weirdly different AST structure
  // than other class members.

  let start: TSESTree.Position;

  if (node.decorators.length === 0) {
    start = structuredClone(node.loc.start);
  } else {
    const lastDecorator = node.decorators[node.decorators.length - 1];
    const nextToken = nullThrows(
      sourceCode.getTokenAfter(lastDecorator),
      NullThrowsReasons.MissingToken('token', 'last decorator'),
    );
    start = structuredClone(nextToken.loc.start);
  }

  const end = sourceCode.getLocFromIndex(
    node.parameter.range[0] + nodeName.length,
  );

  return {
    end,
    start,
  };
}
```
</details>

- **JSDoc**:
```ts
/**
 * Generates report loc suitable for reporting on how a parameter property is
 * declared.
 *
 * ```ts
 * class A {
 *   constructor(private property: string = 'value') {
 *               ~~~~~~~~~~~~~~~~
 *   }
 * ```
 */
```

- **Parameters**:
  - `sourceCode: Readonly<TSESLint.SourceCode>`
  - `node: TSESTree.TSParameterProperty`
  - `nodeName: string`
- **Return Type**: `TSESTree.SourceLocation`
- **Calls**:
  - `structuredClone`
  - `nullThrows (from @typescript-eslint/utils/eslint-utils)`
  - `sourceCode.getTokenAfter`
  - `NullThrowsReasons.MissingToken`
  - `sourceCode.getLocFromIndex`
- **Internal Comments**:
```
// Parameter properties have a weirdly different AST structure (x2)
// than other class members. (x2)
```


---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---