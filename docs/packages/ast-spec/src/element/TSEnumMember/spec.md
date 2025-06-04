[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

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