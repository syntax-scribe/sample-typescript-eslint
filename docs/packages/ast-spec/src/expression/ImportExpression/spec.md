[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

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
📂 **`packages/ast-spec/src/expression/ImportExpression/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Expression` | `../../unions/Expression` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ImportExpression`

<details><summary>Interface Code</summary>

```ts
export interface ImportExpression extends BaseNode {
  type: AST_NODE_TYPES.ImportExpression;
  /**
   * The attributes declared for the dynamic import.
   * @example
   * ```ts
   * import('mod', \{ assert: \{ type: 'json' \} \});
   * ```
   * @deprecated Replaced with {@link `options`}.
   */
  attributes: Expression | null;
  /**
   * The options bag declared for the dynamic import.
   * @example
   * ```ts
   * import('mod', \{ assert: \{ type: 'json' \} \});
   * ```
   */
  options: Expression | null;
  source: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ImportExpression` | ✗ |  |
| `attributes` | `Expression | null` | ✗ |  |
| `options` | `Expression | null` | ✗ |  |
| `source` | `Expression` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---