[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 2
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/PropertyDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `ClassPropertyDefinitionNonComputedNameBase` | `../../base/PropertyDefinitionBase` |
| `PropertyDefinitionComputedNameBase` | `../../base/PropertyDefinitionBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


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