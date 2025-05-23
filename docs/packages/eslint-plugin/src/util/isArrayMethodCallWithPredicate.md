[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `isArrayMethodCallWithPredicate.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/util/isArrayMethodCallWithPredicate.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleContext` | `@typescript-eslint/utils/ts-eslint` |
| `getConstrainedTypeAtLocation` | `@typescript-eslint/type-utils` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `getStaticMemberAccessValue` | `./misc` |


---

## Functions

### `isArrayMethodCallWithPredicate(context: RuleContext<string, unknown[]>, services: ParserServicesWithTypeInformation, node: TSESTree.CallExpression): boolean`

<details><summary>Code</summary>

```ts
export function isArrayMethodCallWithPredicate(
  context: RuleContext<string, unknown[]>,
  services: ParserServicesWithTypeInformation,
  node: TSESTree.CallExpression,
): boolean {
  if (node.callee.type !== AST_NODE_TYPES.MemberExpression) {
    return false;
  }

  const staticAccessValue = getStaticMemberAccessValue(node.callee, context);

  if (!ARRAY_PREDICATE_FUNCTIONS.has(staticAccessValue)) {
    return false;
  }

  const checker = services.program.getTypeChecker();
  const type = getConstrainedTypeAtLocation(services, node.callee.object);
  return tsutils
    .unionConstituents(type)
    .flatMap(part => tsutils.intersectionConstituents(part))
    .some(t => checker.isArrayType(t) || checker.isTupleType(t));
}
```
</details>

- **Parameters**:
  - `context: RuleContext<string, unknown[]>`
  - `services: ParserServicesWithTypeInformation`
  - `node: TSESTree.CallExpression`
- **Return Type**: `boolean`
- **Calls**:
  - `getStaticMemberAccessValue (from ./misc)`
  - `ARRAY_PREDICATE_FUNCTIONS.has`
  - `services.program.getTypeChecker`
  - `getConstrainedTypeAtLocation (from @typescript-eslint/type-utils)`
  - `tsutils
    .unionConstituents(type)
    .flatMap(part => tsutils.intersectionConstituents(part))
    .some`
  - `checker.isArrayType`
  - `checker.isTupleType`

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