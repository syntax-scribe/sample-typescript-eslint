[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSHeritageBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/TSHeritageBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSTypeParameterInstantiation` | `../special/TSTypeParameterInstantiation/spec` |
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSHeritageBase`

<details><summary>Interface Code</summary>

```ts
export interface TSHeritageBase extends BaseNode {
  // TODO(#1852) - this should be restricted to MemberExpression | Identifier
  expression: Expression;
  typeArguments: TSTypeParameterInstantiation | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `expression` | `Expression` | ✗ |  |
| `typeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---