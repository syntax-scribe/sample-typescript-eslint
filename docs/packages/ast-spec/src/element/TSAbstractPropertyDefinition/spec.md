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
📂 **`packages/ast-spec/src/element/TSAbstractPropertyDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `PropertyDefinitionComputedNameBase` | `../../base/PropertyDefinitionBase` |
| `PropertyDefinitionNonComputedNameBase` | `../../base/PropertyDefinitionBase` |


---

## Interfaces

### `TSAbstractPropertyDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractPropertyDefinitionComputedName
  extends PropertyDefinitionComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractPropertyDefinition;
  value: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractPropertyDefinition` | ✗ |  |
| `value` | `null` | ✗ |  |

### `TSAbstractPropertyDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractPropertyDefinitionNonComputedName
  // this does not extend ClassPropertyDefinitionNonComputedNameBase because abstract private names are not allowed
  extends PropertyDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractPropertyDefinition;
  value: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractPropertyDefinition` | ✗ |  |
| `value` | `null` | ✗ |  |


---

## Type Aliases

### `TSAbstractPropertyDefinition`

```ts
type TSAbstractPropertyDefinition = | TSAbstractPropertyDefinitionComputedName
  | TSAbstractPropertyDefinitionNonComputedName;
```


---