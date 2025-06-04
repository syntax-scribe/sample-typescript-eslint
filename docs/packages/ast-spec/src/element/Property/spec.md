[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 9 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/Property/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `TSEmptyBodyFunctionExpression` | `../../expression/TSEmptyBodyFunctionExpression/spec` |
| `AssignmentPattern` | `../../parameter/AssignmentPattern/spec` |
| `BindingName` | `../../unions/BindingName` |
| `Expression` | `../../unions/Expression` |
| `PropertyName` | `../../unions/PropertyName` |
| `PropertyNameComputed` | `../../unions/PropertyName` |
| `PropertyNameNonComputed` | `../../unions/PropertyName` |


---

## Interfaces

### `PropertyBase`

<details><summary>Interface Code</summary>

```ts
interface PropertyBase extends BaseNode {
  type: AST_NODE_TYPES.Property;
  computed: boolean;
  key: PropertyName;
  kind: 'get' | 'init' | 'set';
  method: boolean;
  optional: boolean;
  shorthand: boolean;
  value:
    | AssignmentPattern
    | BindingName
    | Expression
    | TSEmptyBodyFunctionExpression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.Property` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `key` | `PropertyName` | ✗ |  |
| `kind` | `'get' | 'init' | 'set'` | ✗ |  |
| `method` | `boolean` | ✗ |  |
| `optional` | `boolean` | ✗ |  |
| `shorthand` | `boolean` | ✗ |  |
| `value` | `| AssignmentPattern
    | BindingName
    | Expression
    | TSEmptyBodyFunctionExpression` | ✗ |  |

### `PropertyComputedName`

<details><summary>Interface Code</summary>

```ts
export interface PropertyComputedName extends PropertyBase {
  computed: true;
  key: PropertyNameComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `true` | ✗ |  |
| `key` | `PropertyNameComputed` | ✗ |  |

### `PropertyNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface PropertyNonComputedName extends PropertyBase {
  computed: false;
  key: PropertyNameNonComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `false` | ✗ |  |
| `key` | `PropertyNameNonComputed` | ✗ |  |


---

## Type Aliases

### `Property`

```ts
type Property = PropertyComputedName | PropertyNonComputedName;
```


---