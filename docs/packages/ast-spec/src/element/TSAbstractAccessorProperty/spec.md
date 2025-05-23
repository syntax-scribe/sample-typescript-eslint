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
📂 **`packages/ast-spec/src/element/TSAbstractAccessorProperty/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `PropertyDefinitionComputedNameBase` | `../../base/PropertyDefinitionBase` |
| `PropertyDefinitionNonComputedNameBase` | `../../base/PropertyDefinitionBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSAbstractAccessorPropertyComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractAccessorPropertyComputedName
  extends PropertyDefinitionComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractAccessorProperty;
  value: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractAccessorProperty` | ✗ |  |
| `value` | `null` | ✗ |  |

### `TSAbstractAccessorPropertyNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractAccessorPropertyNonComputedName
  // this does not extend ClassPropertyDefinitionNonComputedNameBase because abstract private names are not allowed
  extends PropertyDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractAccessorProperty;
  value: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractAccessorProperty` | ✗ |  |
| `value` | `null` | ✗ |  |


---

## Type Aliases

### `TSAbstractAccessorProperty`

```ts
type TSAbstractAccessorProperty = | TSAbstractAccessorPropertyComputedName
  | TSAbstractAccessorPropertyNonComputedName;
```


---