[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `getMemberHeadLoc.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
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
📂 **`packages/eslint-plugin/src/util/getMemberHeadLoc.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `nullThrows` | `@typescript-eslint/utils/eslint-utils` |
| `NullThrowsReasons` | `@typescript-eslint/utils/eslint-utils` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `start` | `TSESTree.Position` | let/var | `*not shown*` | ✗ |
| `lastDecorator` | `any` | const | `node.decorators[node.decorators.length - 1]` | ✗ |
| `end` | `TSESTree.Position` | let/var | `*not shown*` | ✗ |
| `start` | `TSESTree.Position` | let/var | `*not shown*` | ✗ |
| `lastDecorator` | `any` | const | `node.decorators[node.decorators.length - 1]` | ✗ |


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