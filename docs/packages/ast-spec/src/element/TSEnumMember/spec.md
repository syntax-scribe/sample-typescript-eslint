[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 3
- **Type Aliases**: 1

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/TSEnumMember/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |
| `PropertyNameComputed` | `../../unions/PropertyName` |
| `PropertyNameNonComputed` | `../../unions/PropertyName` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSEnumMemberBase`

<details><summary>Interface Code</summary>

```ts
interface TSEnumMemberBase extends BaseNode {
  type: AST_NODE_TYPES.TSEnumMember;
  computed: boolean;
  id:
    | PropertyNameComputed // this should only happen in semantically invalid code (ts error 1164)
    | PropertyNameNonComputed;
  initializer: Expression | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSEnumMember` | ✗ |  |
| `computed` | `boolean` | ✗ |  |
| `id` | `| PropertyNameComputed // this should only happen in semantically invalid code (ts error 1164)
    | PropertyNameNonComputed` | ✗ |  |
| `initializer` | `Expression | undefined` | ✗ |  |

### `TSEnumMemberComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSEnumMemberComputedName extends TSEnumMemberBase {
  computed: true;
  id: PropertyNameComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `true` | ✗ |  |
| `id` | `PropertyNameComputed` | ✗ |  |

### `TSEnumMemberNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSEnumMemberNonComputedName extends TSEnumMemberBase {
  computed: false;
  id: PropertyNameNonComputed;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `computed` | `false` | ✗ |  |
| `id` | `PropertyNameNonComputed` | ✗ |  |


---

## Type Aliases

### `TSEnumMember`

```ts
type TSEnumMember = | TSEnumMemberComputedName
  | TSEnumMemberNonComputedName;
```


---