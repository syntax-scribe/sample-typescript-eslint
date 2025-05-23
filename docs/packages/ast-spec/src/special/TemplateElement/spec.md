[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/TemplateElement/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `TemplateElement`

<details><summary>Interface Code</summary>

```ts
export interface TemplateElement extends BaseNode {
  type: AST_NODE_TYPES.TemplateElement;
  tail: boolean;
  value: {
    cooked: string;
    raw: string;
  };
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TemplateElement` | ✗ |  |
| `tail` | `boolean` | ✗ |  |
| `value` | `{
    cooked: string;
    raw: string;
  }` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---