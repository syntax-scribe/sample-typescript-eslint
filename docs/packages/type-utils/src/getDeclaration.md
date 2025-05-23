[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getDeclaration.ts`

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
📂 **`packages/type-utils/src/getDeclaration.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `ParserServicesWithTypeInformation` | `@typescript-eslint/typescript-estree` |
| `TSESTree` | `@typescript-eslint/typescript-estree` |


---

## Functions

### `getDeclaration(services: ParserServicesWithTypeInformation, node: TSESTree.Node): ts.Declaration | null`

<details><summary>Code</summary>

```ts
export function getDeclaration(
  services: ParserServicesWithTypeInformation,
  node: TSESTree.Node,
): ts.Declaration | null {
  const symbol = services.getSymbolAtLocation(node);
  if (!symbol) {
    return null;
  }
  const declarations = symbol.getDeclarations();
  return declarations?.[0] ?? null;
}
```
</details>

- **JSDoc**:
```ts
/**
 * Gets the declaration for the given variable
 */
```

- **Parameters**:
  - `services: ParserServicesWithTypeInformation`
  - `node: TSESTree.Node`
- **Return Type**: `ts.Declaration | null`
- **Calls**:
  - `services.getSymbolAtLocation`
  - `symbol.getDeclarations`

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