[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/type/TSMappedType/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `TSTypeParameter` | `../../special/TSTypeParameter/spec` |
| `TypeNode` | `../../unions/TypeNode` |


---

## Interfaces

### `TSMappedType`

<details><summary>Interface Code</summary>

```ts
export interface TSMappedType extends BaseNode {
  type: AST_NODE_TYPES.TSMappedType;
  constraint: TypeNode;
  key: Identifier;
  nameType: TypeNode | null;
  optional: boolean | '+' | '-' | undefined;
  readonly: boolean | '+' | '-' | undefined;
  typeAnnotation: TypeNode | undefined;
  /** @deprecated Use {@link `constraint`} and {@link `key`} instead. */
  typeParameter: TSTypeParameter;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSMappedType` | ✗ |  |
| `constraint` | `TypeNode` | ✗ |  |
| `key` | `Identifier` | ✗ |  |
| `nameType` | `TypeNode | null` | ✗ |  |
| `optional` | `boolean | '+' | '-' | undefined` | ✗ |  |
| `readonly` | `boolean | '+' | '-' | undefined` | ✗ |  |
| `typeAnnotation` | `TypeNode | undefined` | ✗ |  |
| `typeParameter` | `TSTypeParameter` | ✗ |  |


---