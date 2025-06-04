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