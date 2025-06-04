[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/TSAbstractMethodDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `MethodDefinitionComputedNameBase` | `../../base/MethodDefinitionBase` |
| `MethodDefinitionNonComputedNameBase` | `../../base/MethodDefinitionBase` |


---

## Interfaces

### `TSAbstractMethodDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractMethodDefinitionComputedName
  extends MethodDefinitionComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractMethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractMethodDefinition` | ✗ |  |

### `TSAbstractMethodDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractMethodDefinitionNonComputedName
  // this does not extend ClassMethodDefinitionNonComputedNameBase because abstract private names are not allowed
  extends MethodDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractMethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractMethodDefinition` | ✗ |  |


---

## Type Aliases

### `TSAbstractMethodDefinition`

```ts
type TSAbstractMethodDefinition = | TSAbstractMethodDefinitionComputedName
  | TSAbstractMethodDefinitionNonComputedName;
```


---