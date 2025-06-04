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
📂 **`packages/ast-spec/src/element/MethodDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `ClassMethodDefinitionNonComputedNameBase` | `../../base/MethodDefinitionBase` |
| `MethodDefinitionComputedNameBase` | `../../base/MethodDefinitionBase` |


---

## Interfaces

### `MethodDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface MethodDefinitionComputedName
  extends MethodDefinitionComputedNameBase {
  type: AST_NODE_TYPES.MethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.MethodDefinition` | ✗ |  |

### `MethodDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface MethodDefinitionNonComputedName
  extends ClassMethodDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.MethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.MethodDefinition` | ✗ |  |


---

## Type Aliases

### `MethodDefinition`

```ts
type MethodDefinition = | MethodDefinitionComputedName
  | MethodDefinitionNonComputedName;
```


---