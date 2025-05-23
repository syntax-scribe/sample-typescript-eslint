[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `discriminateAnyType.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/discriminateAnyType.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `isTypeAnyType` | `./predicates` |
| `isTypeAnyArrayType` | `./predicates` |


---

## Functions

### `discriminateAnyType(type: ts.Type, checker: ts.TypeChecker, program: ts.Program, tsNode: ts.Node): AnyType`

<details><summary>Code</summary>

```ts
export function discriminateAnyType(
  type: ts.Type,
  checker: ts.TypeChecker,
  program: ts.Program,
  tsNode: ts.Node,
): AnyType {
  return discriminateAnyTypeWorker(type, checker, program, tsNode, new Set());
}
```
</details>

- **JSDoc**:
```ts
/**
 * @returns `AnyType.Any` if the type is `any`, `AnyType.AnyArray` if the type is `any[]` or `readonly any[]`, `AnyType.PromiseAny` if the type is `Promise<any>`,
 *          otherwise it returns `AnyType.Safe`.
 */
```

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
  - `program: ts.Program`
  - `tsNode: ts.Node`
- **Return Type**: `AnyType`
- **Calls**:
  - `discriminateAnyTypeWorker`
### `discriminateAnyTypeWorker(type: ts.Type, checker: ts.TypeChecker, program: ts.Program, tsNode: ts.Node, visited: Set<ts.Type>): AnyType`

<details><summary>Code</summary>

```ts
function discriminateAnyTypeWorker(
  type: ts.Type,
  checker: ts.TypeChecker,
  program: ts.Program,
  tsNode: ts.Node,
  visited: Set<ts.Type>,
) {
  if (visited.has(type)) {
    return AnyType.Safe;
  }
  visited.add(type);
  if (isTypeAnyType(type)) {
    return AnyType.Any;
  }
  if (isTypeAnyArrayType(type, checker)) {
    return AnyType.AnyArray;
  }
  for (const part of tsutils.typeConstituents(type)) {
    if (tsutils.isThenableType(checker, tsNode, part)) {
      const awaitedType = checker.getAwaitedType(part);
      if (awaitedType) {
        const awaitedAnyType = discriminateAnyTypeWorker(
          awaitedType,
          checker,
          program,
          tsNode,
          visited,
        );
        if (awaitedAnyType === AnyType.Any) {
          return AnyType.PromiseAny;
        }
      }
    }
  }

  return AnyType.Safe;
}
```
</details>

- **Parameters**:
  - `type: ts.Type`
  - `checker: ts.TypeChecker`
  - `program: ts.Program`
  - `tsNode: ts.Node`
  - `visited: Set<ts.Type>`
- **Return Type**: `AnyType`
- **Calls**:
  - `visited.has`
  - `visited.add`
  - `isTypeAnyType (from ./predicates)`
  - `isTypeAnyArrayType (from ./predicates)`
  - `tsutils.typeConstituents`
  - `tsutils.isThenableType`
  - `checker.getAwaitedType`
  - `discriminateAnyTypeWorker`

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