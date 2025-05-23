[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getConstrainedTypeAtLocation.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/type-utils/src/getConstrainedTypeAtLocation.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/typescript-estree` |
| `TSESTree` | `@typescript-eslint/typescript-estree` |


---

## Functions

### `getConstrainedTypeAtLocation(services: ParserServicesWithTypeInformation, node: TSESTree.Node): ts.Type`

<details><summary>Code</summary>

```ts
export function getConstrainedTypeAtLocation(
  services: ParserServicesWithTypeInformation,
  node: TSESTree.Node,
): ts.Type {
  const nodeType = services.getTypeAtLocation(node);
  const constrained = services.program
    .getTypeChecker()
    .getBaseConstraintOfType(nodeType);

  return constrained ?? nodeType;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Resolves the given node's type. Will return the type's generic constraint, if it has one.
 *
 * Warning - if the type is generic and does _not_ have a constraint, the type will be
 * returned as-is, rather than returning an `unknown` type. This can be checked
 * for by checking for the type flag ts.TypeFlags.TypeParameter.
 *
 * @see https://github.com/typescript-eslint/typescript-eslint/issues/10438
 */
```

- **Parameters**:
  - `services: ParserServicesWithTypeInformation`
  - `node: TSESTree.Node`
- **Return Type**: `ts.Type`
- **Calls**:
  - `services.getTypeAtLocation`
  - `services.program
    .getTypeChecker()
    .getBaseConstraintOfType`

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