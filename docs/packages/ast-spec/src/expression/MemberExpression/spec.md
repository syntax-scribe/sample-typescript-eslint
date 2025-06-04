[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 5 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/expression/MemberExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `PrivateIdentifier` | `../../special/PrivateIdentifier/spec` |
| `Expression` | `../../unions/Expression` |
| `Identifier` | `../Identifier/spec` |


---

## Interfaces

### `MemberExpressionBase`

<details><summary>Interface Code</summary>

```ts
interface MemberExpressionBase extends BaseNode {
  computed: boolean;
  object: Expression;
  optional: boolean;
  property: Expression | Identifier | PrivateIdentifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `boolean` | ✗ |  |
| `object` | `Expression` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `property` | `Expression | Identifier | PrivateIdentifier` | ✗ |  |

### `MemberExpressionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface MemberExpressionComputedName extends MemberExpressionBase {
  type: AST_NODE_TYPES.MemberExpression;
  computed: true;
  property: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.MemberExpression` | ✗ |  |
| `computed` | `true` | ✗ |  |
| `property` | `Expression` | ✗ |  |

### `MemberExpressionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface MemberExpressionNonComputedName extends MemberExpressionBase {
  type: AST_NODE_TYPES.MemberExpression;
  computed: false;
  property: Identifier | PrivateIdentifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.MemberExpression` | ✗ |  |
| `computed` | `false` | ✗ |  |
| `property` | `Identifier | PrivateIdentifier` | ✗ |  |


---

## Type Aliases

### `MemberExpression`

```ts
type MemberExpression = | MemberExpressionComputedName
  | MemberExpressionNonComputedName;
```


---