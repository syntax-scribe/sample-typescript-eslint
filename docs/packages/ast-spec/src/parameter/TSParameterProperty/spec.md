[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 7
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/parameter/TSParameterProperty/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `Accessibility` | `../../base/Accessibility` |
| `BaseNode` | `../../base/BaseNode` |
| `Decorator` | `../../special/Decorator/spec` |
| `BindingName` | `../../unions/BindingName` |
| `AssignmentPattern` | `../AssignmentPattern/spec` |
| `RestElement` | `../RestElement/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TSParameterProperty`

<details><summary>Interface Code</summary>

```ts
export interface TSParameterProperty extends BaseNode {
  type: AST_NODE_TYPES.TSParameterProperty;
  accessibility: Accessibility | undefined;
  decorators: Decorator[];
  override: boolean;
  parameter: AssignmentPattern | BindingName | RestElement;
  readonly: boolean;
  static: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSParameterProperty` | ✗ |  |
| `accessibility` | `Accessibility | undefined` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `override` | `boolean` | ✗ |  |
| `parameter` | `AssignmentPattern | BindingName | RestElement` | ✗ |  |
| `readonly` | `boolean` | ✗ |  |
| `static` | `boolean` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---