[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 6 |
| 📑 Type Aliases | 3 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/special/VariableDeclarator/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `BindingName` | `../../unions/BindingName` |
| `Expression` | `../../unions/Expression` |


---


---

## Interfaces

### `VariableDeclaratorBase`

<details><summary>Interface Code</summary>

```ts
interface VariableDeclaratorBase extends BaseNode {
  type: AST_NODE_TYPES.VariableDeclarator;
  /**
   * Whether there's definite assignment assertion (`let x!: number`).
   * If `true`, then: `id` must be an identifier with a type annotation,
   * `init` must be `null`, and the declarator must be a `var`/`let` declarator.
   */
  definite: boolean;
  /**
   * The name(s) of the variable(s).
   */
  id: BindingName;
  /**
   * The initializer expression of the variable. Must be present for `const` unless
   * in a `declare const`.
   */
  init: Expression | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.VariableDeclarator` | ✗ |  |
| `definite` | `boolean` | ✗ |  |
| `id` | `BindingName` | ✗ |  |
| `init` | `Expression | null` | ✗ |  |

### `VariableDeclaratorNoInit`

<details><summary>Interface Code</summary>

```ts
export interface VariableDeclaratorNoInit extends VariableDeclaratorBase {
  definite: false;
  init: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `definite` | `false` | ✗ |  |
| `init` | `null` | ✗ |  |

### `VariableDeclaratorMaybeInit`

<details><summary>Interface Code</summary>

```ts
export interface VariableDeclaratorMaybeInit extends VariableDeclaratorBase {
  definite: false;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `definite` | `false` | ✗ |  |

### `VariableDeclaratorDefiniteAssignment`

<details><summary>Interface Code</summary>

```ts
export interface VariableDeclaratorDefiniteAssignment
  extends VariableDeclaratorBase {
  definite: true;
  /**
   * The name of the variable. Must have a type annotation.
   */
  id: Identifier;
  init: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `definite` | `true` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `init` | `null` | ✗ |  |

### `UsingInNormalContextDeclarator`

<details><summary>Interface Code</summary>

```ts
export interface UsingInNormalContextDeclarator extends VariableDeclaratorBase {
  definite: false;
  id: Identifier;
  init: Expression;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `definite` | `false` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `init` | `Expression` | ✗ |  |

### `UsingInForOfDeclarator`

<details><summary>Interface Code</summary>

```ts
export interface UsingInForOfDeclarator extends VariableDeclaratorBase {
  definite: false;
  id: Identifier;
  init: null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `definite` | `false` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `init` | `null` | ✗ |  |


---

## Type Aliases

### `LetOrConstOrVarDeclarator`

```ts
type LetOrConstOrVarDeclarator = | VariableDeclaratorDefiniteAssignment
  | VariableDeclaratorMaybeInit
  | VariableDeclaratorNoInit;
```

### `UsingDeclarator`

```ts
type UsingDeclarator = | UsingInForOfDeclarator
  | UsingInNormalContextDeclarator;
```

### `VariableDeclarator`

```ts
type VariableDeclarator = LetOrConstOrVarDeclarator | UsingDeclarator;
```


---