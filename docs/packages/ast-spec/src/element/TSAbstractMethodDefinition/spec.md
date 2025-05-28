[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/element/TSAbstractMethodDefinition/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `MethodDefinitionComputedNameBase` | `../../base/MethodDefinitionBase` |
| `MethodDefinitionNonComputedNameBase` | `../../base/MethodDefinitionBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `TSAbstractMethodDefinitionComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractMethodDefinitionComputedName
  extends MethodDefinitionComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractMethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractMethodDefinition` | ✗ |  |

### `TSAbstractMethodDefinitionNonComputedName`

<details><summary>Interface Code</summary>

```ts
export interface TSAbstractMethodDefinitionNonComputedName
  // this does not extend ClassMethodDefinitionNonComputedNameBase because abstract private names are not allowed
  extends MethodDefinitionNonComputedNameBase {
  type: AST_NODE_TYPES.TSAbstractMethodDefinition;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSAbstractMethodDefinition` | ✗ |  |


---

## Type Aliases

### `TSAbstractMethodDefinition`

```ts
type TSAbstractMethodDefinition = | TSAbstractMethodDefinitionComputedName
  | TSAbstractMethodDefinitionNonComputedName;
```


---