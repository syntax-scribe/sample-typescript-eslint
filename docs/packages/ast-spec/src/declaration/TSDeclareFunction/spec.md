[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 2 |
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
📂 **`packages/ast-spec/src/declaration/TSDeclareFunction/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `FunctionBase` | `../../base/FunctionBase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Interfaces

### `TSDeclareFunctionBase`

<details><summary>Interface Code</summary>

```ts
interface TSDeclareFunctionBase extends FunctionBase {
  type: AST_NODE_TYPES.TSDeclareFunction;
  /**
   * TS1183: An implementation cannot be declared in ambient contexts.
   */
  body: undefined;
  /**
   * Whether the declaration has `declare` modifier.
   */
  declare: boolean;
  expression: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSDeclareFunction` | ✗ |  |
| `body` | `undefined` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `expression` | `false` | ✗ |  |

### `TSDeclareFunctionWithDeclare`

<details><summary>Interface Code</summary>

```ts
export interface TSDeclareFunctionWithDeclare extends TSDeclareFunctionBase {
  /**
   * TS1040: 'async' modifier cannot be used in an ambient context.
   */
  async: false;
  declare: true;
  /**
   * TS1221: Generators are not allowed in an ambient context.
   */
  generator: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `async` | `false` | ✗ |  |
| `declare` | `true` | ✗ |  |
| `generator` | `false` | ✗ |  |

### `TSDeclareFunctionNoDeclare`

<details><summary>Interface Code</summary>

```ts
export interface TSDeclareFunctionNoDeclare extends TSDeclareFunctionBase {
  declare: false;
  /**
   * - TS1221: Generators are not allowed in an ambient context.
   * - TS1222: An overload signature cannot be declared as a generator.
   */
  generator: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declare` | `false` | ✗ |  |
| `generator` | `false` | ✗ |  |


---

## Type Aliases

### `TSDeclareFunction`

```ts
type TSDeclareFunction = | TSDeclareFunctionNoDeclare
  | TSDeclareFunctionWithDeclare;
```


---