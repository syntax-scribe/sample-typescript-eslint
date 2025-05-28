[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `isUnsafeAssignment.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 4 |
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
📂 **`packages/type-utils/src/isUnsafeAssignment.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `isTypeAnyType` | `./predicates` |
| `isTypeUnknownType` | `./predicates` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `typeArguments` | `any` | const | `type.typeArguments ?? []` | ✗ |
| `receiverTypeArguments` | `any` | const | `receiver.typeArguments ?? []` | ✗ |
| `arg` | `any` | const | `typeArguments[i]` | ✗ |
| `receiverArg` | `any` | const | `receiverTypeArguments[i]` | ✗ |


---

## Functions

### `isUnsafeAssignment(type: ts.Type, receiver: ts.Type, checker: ts.TypeChecker, senderNode: TSESTree.Node | null): false | { receiver: ts.Type; sender: ts.Type }`

<details><summary>Code</summary>

```ts
export function isUnsafeAssignment(
  type: ts.Type,
  receiver: ts.Type,
  checker: ts.TypeChecker,
  senderNode: TSESTree.Node | null,
): false | { receiver: ts.Type; sender: ts.Type } {
  return isUnsafeAssignmentWorker(
    type,
    receiver,
    checker,
    senderNode,
    new Map(),
  );
}
```
</details>

- **JSDoc**:
```ts
/**
 * Does a simple check to see if there is an any being assigned to a non-any type.
 *
 * This also checks generic positions to ensure there's no unsafe sub-assignments.
 * Note: in the case of generic positions, it makes the assumption that the two types are the same.
 *
 * @example See tests for examples
 *
 * @returns false if it's safe, or an object with the two types if it's unsafe
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `receiver: ts.Type`
  - `checker: ts.TypeChecker`
  - `senderNode: TSESTree.Node | null`
- **Return Type**: `false | { receiver: ts.Type; sender: ts.Type }`
- **Calls**:
  - `isUnsafeAssignmentWorker`
### `isUnsafeAssignmentWorker(type: ts.Type, receiver: ts.Type, checker: ts.TypeChecker, senderNode: TSESTree.Node | null, visited: Map<ts.Type, Set<ts.Type>>): false | { receiver: ts.Type; sender: ts.Type }`

<details><summary>Code</summary>

```ts
function isUnsafeAssignmentWorker(
  type: ts.Type,
  receiver: ts.Type,
  checker: ts.TypeChecker,
  senderNode: TSESTree.Node | null,
  visited: Map<ts.Type, Set<ts.Type>>,
): false | { receiver: ts.Type; sender: ts.Type } {
  if (isTypeAnyType(type)) {
    // Allow assignment of any ==> unknown.
    if (isTypeUnknownType(receiver)) {
      return false;
    }

    if (!isTypeAnyType(receiver)) {
      return { receiver, sender: type };
    }
  }

  const typeAlreadyVisited = visited.get(type);

  if (typeAlreadyVisited) {
    if (typeAlreadyVisited.has(receiver)) {
      return false;
    }
    typeAlreadyVisited.add(receiver);
  } else {
    visited.set(type, new Set([receiver]));
  }

  if (tsutils.isTypeReference(type) && tsutils.isTypeReference(receiver)) {
    // TODO - figure out how to handle cases like this,
    // where the types are assignable, but not the same type
    /*
    function foo(): ReadonlySet<number> { return new Set<any>(); }

    // and

    type Test<T> = { prop: T }
    type Test2 = { prop: string }
    declare const a: Test<any>;
    const b: Test2 = a;
    */

    if (type.target !== receiver.target) {
      // if the type references are different, assume safe, as we won't know how to compare the two types
      // the generic positions might not be equivalent for both types
      return false;
    }

    if (
      senderNode?.type === AST_NODE_TYPES.NewExpression &&
      senderNode.callee.type === AST_NODE_TYPES.Identifier &&
      senderNode.callee.name === 'Map' &&
      senderNode.arguments.length === 0 &&
      senderNode.typeArguments == null
    ) {
      // special case to handle `new Map()`
      // unfortunately Map's default empty constructor is typed to return `Map<any, any>` :(
      // https://github.com/typescript-eslint/typescript-eslint/issues/2109#issuecomment-634144396
      return false;
    }

    const typeArguments = type.typeArguments ?? [];
    const receiverTypeArguments = receiver.typeArguments ?? [];

    for (let i = 0; i < typeArguments.length; i += 1) {
      const arg = typeArguments[i];
      const receiverArg = receiverTypeArguments[i];

      const unsafe = isUnsafeAssignmentWorker(
        arg,
        receiverArg,
        checker,
        senderNode,
        visited,
      );
      if (unsafe) {
        return { receiver, sender: type };
      }
    }

    return false;
  }

  return false;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `receiver: ts.Type`
  - `checker: ts.TypeChecker`
  - `senderNode: TSESTree.Node | null`
  - `visited: Map<ts.Type, Set<ts.Type>>`
- **Return Type**: `false | { receiver: ts.Type; sender: ts.Type }`
- **Calls**:
  - `isTypeAnyType (from ./predicates)`
  - `isTypeUnknownType (from ./predicates)`
  - `visited.get`
  - `typeAlreadyVisited.has`
  - `typeAlreadyVisited.add`
  - `visited.set`
  - `tsutils.isTypeReference`
  - `isUnsafeAssignmentWorker`
- **Internal Comments**:
```
// Allow assignment of any ==> unknown.
// TODO - figure out how to handle cases like this,
// where the types are assignable, but not the same type
/*
    function foo(): ReadonlySet<number> { return new Set<any>(); }

    // and

    type Test<T> = { prop: T }
    type Test2 = { prop: string }
    declare const a: Test<any>;
    const b: Test2 = a;
    */
// if the type references are different, assume safe, as we won't know how to compare the two types
// the generic positions might not be equivalent for both types
// special case to handle `new Map()`
// unfortunately Map's default empty constructor is typed to return `Map<any, any>` :(
// https://github.com/typescript-eslint/typescript-eslint/issues/2109#issuecomment-634144396
```


---