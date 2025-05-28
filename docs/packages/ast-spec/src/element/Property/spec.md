[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 9 |
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

## 🔧 Functions

> No functions found in this file.


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