[⬅️ Back to Table of Contents](../../../index.md)

# 📄 `getDeclaration.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

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