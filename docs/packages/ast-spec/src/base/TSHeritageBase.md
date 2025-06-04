[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `TSHeritageBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/TSHeritageBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSTypeParameterInstantiation` | `../special/TSTypeParameterInstantiation/spec` |
| `Expression` | `../unions/Expression` |
| `BaseNode` | `./BaseNode` |


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