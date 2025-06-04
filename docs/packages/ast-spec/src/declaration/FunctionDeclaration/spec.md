[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 4 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/FunctionDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `FunctionBase` | `../../base/FunctionBase` |
| `Identifier` | `../../expression/Identifier/spec` |
| `BlockStatement` | `../../statement/BlockStatement/spec` |


---

## Interfaces

### `FunctionDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface FunctionDeclarationBase extends FunctionBase {
  type: AST_NODE_TYPES.FunctionDeclaration;
  body: BlockStatement;
  declare: false;
  expression: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.FunctionDeclaration` | ✗ |  |
| `body` | `BlockStatement` | ✗ |  |
| `declare` | `false` | ✗ |  |
| `expression` | `false` | ✗ |  |

### `FunctionDeclarationWithName`

<details><summary>Interface Code</summary>

```ts
export interface FunctionDeclarationWithName extends FunctionDeclarationBase {
  id: Identifier;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `id` | `Identifier` | ✗ |  |

### `FunctionDeclarationWithOptionalName`

<details><summary>Interface Code</summary>

```ts
export interface FunctionDeclarationWithOptionalName
  extends FunctionDeclarationBase {
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

### `FunctionDeclaration`

```ts
type FunctionDeclaration = | FunctionDeclarationWithName
  | FunctionDeclarationWithOptionalName;
```


---