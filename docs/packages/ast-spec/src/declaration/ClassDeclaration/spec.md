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
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/ClassDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `ClassBase` | `../../base/ClassBase` |
| `Identifier` | `../../expression/Identifier/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `ClassDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface ClassDeclarationBase extends ClassBase {
  type: AST_NODE_TYPES.ClassDeclaration;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.ClassDeclaration` | ✗ |  |

### `ClassDeclarationWithName`

<details><summary>Interface Code</summary>

```ts
export interface ClassDeclarationWithName extends ClassDeclarationBase {
  id: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `id` | `Identifier` | ✗ |  |

### `ClassDeclarationWithOptionalName`

<details><summary>Interface Code</summary>

```ts
export interface ClassDeclarationWithOptionalName extends ClassDeclarationBase {
  id: Identifier | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `id` | `Identifier | null` | ✗ |  |


---

## Type Aliases

### `ClassDeclaration`

```ts
type ClassDeclaration = | ClassDeclarationWithName
  | ClassDeclarationWithOptionalName;
```


---