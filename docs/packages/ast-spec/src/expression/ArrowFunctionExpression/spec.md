[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 7 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/ArrowFunctionExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSTypeAnnotation` | `../../special/TSTypeAnnotation/spec` |
| `TSTypeParameterDeclaration` | `../../special/TSTypeParameterDeclaration/spec` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |
| `Expression` | `../../unions/Expression` |
| `Parameter` | `../../unions/Parameter` |


---

## Interfaces

### `ArrowFunctionExpression`

<details><summary>Interface Code</summary>

```ts
export interface ArrowFunctionExpression extends BaseNode {
  type: AST_NODE_TYPES.ArrowFunctionExpression;
  async: boolean;
  body: BlockStatement | Expression;
  expression: boolean;
  generator: boolean;
  id: null;
  params: Parameter[];
  returnType: TSTypeAnnotation | undefined;
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ArrowFunctionExpression` | ✗ |  |
| `async` | `boolean` | ✗ |  |
| `body` | `BlockStatement | Expression` | ✗ |  |
| `expression` | `boolean` | ✗ |  |
| `generator` | `boolean` | ✗ |  |
| `id` | `null` | ✗ |  |
| `params` | `Parameter[]` | ✗ |  |
| `returnType` | `TSTypeAnnotation | undefined` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---