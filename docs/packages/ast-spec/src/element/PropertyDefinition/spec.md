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
📂 **`packages/ast-spec/src/element/PropertyDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `ClassPropertyDefinitionNonComputedNameBase` | `../../base/PropertyDefinitionBase` |
| `PropertyDefinitionComputedNameBase` | `../../base/PropertyDefinitionBase` |


---

## Interfaces

### `PropertyDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface PropertyDefinitionComputedName
  extends PropertyDefinitionComputedNameBase {
  type: AST_NODE_TYPES.PropertyDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.PropertyDefinition` | ✗ |  |

### `PropertyDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface PropertyDefinitionNonComputedName
  extends ClassPropertyDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.PropertyDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.PropertyDefinition` | ✗ |  |


---

## Type Aliases

### `PropertyDefinition`

```ts
type PropertyDefinition = | PropertyDefinitionComputedName
  | PropertyDefinitionNonComputedName;
```


---