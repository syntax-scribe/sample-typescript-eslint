[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSImportType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `ObjectExpression` | `../../expression/ObjectExpression/spec` |
| `TSTypeParameterInstantiation` | `../../special/TSTypeParameterInstantiation/spec` |
| `EntityName` | `../../unions/EntityName` |
| `TypeNode` | `../../unions/TypeNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSImportType`

<details><summary>Interface Code</summary>

```ts
export interface TSImportType extends BaseNode {
  type: AST_NODE_TYPES.TSImportType;
  argument: TypeNode;
  options: ObjectExpression | null;
  qualifier: EntityName | null;
  typeArguments: TSTypeParameterInstantiation | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSImportType` | ✗ |  |
| `argument` | `TypeNode` | ✗ |  |
| `options` | `ObjectExpression | null` | ✗ |  |
| `qualifier` | `EntityName | null` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | null` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---