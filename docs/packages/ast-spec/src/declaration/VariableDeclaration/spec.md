[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 7
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/VariableDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `LetOrConstOrVarDeclarator` | `../../special/VariableDeclarator/spec` |
| `UsingInForOfDeclarator` | `../../special/VariableDeclarator/spec` |
| `UsingInNormalContextDeclarator` | `../../special/VariableDeclarator/spec` |
| `VariableDeclaratorDefiniteAssignment` | `../../special/VariableDeclarator/spec` |
| `VariableDeclaratorMaybeInit` | `../../special/VariableDeclarator/spec` |
| `VariableDeclaratorNoInit` | `../../special/VariableDeclarator/spec` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `LetOrConstOrVarDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface LetOrConstOrVarDeclarationBase extends BaseNode {
  type: AST_NODE_TYPES.VariableDeclaration;
  /**
   * The variables declared by this declaration.
   * Always non-empty.
   * @example
   * ```ts
   * let x;
   * let y, z;
   * ```
   */
  declarations: LetOrConstOrVarDeclarator[];
  /**
   * Whether the declaration is `declare`d
   * @example
   * ```ts
   * declare const x = 1;
   * ```
   */
  declare: boolean;
  /**
   * The keyword used to declare the variable(s)
   * @example
   * ```ts
   * const x = 1;
   * let y = 2;
   * var z = 3;
   * ```
   */
  kind: 'const' | 'let' | 'var';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.VariableDeclaration` | ✗ |  |
| `declarations` | `LetOrConstOrVarDeclarator[]` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `kind` | `'const' | 'let' | 'var'` | ✗ |  |

### `LetOrVarDeclaredDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface LetOrVarDeclaredDeclaration
  extends LetOrConstOrVarDeclarationBase {
  /**
   * In a `declare let` declaration, the declarators must not have definite assignment
   * assertions or initializers.
   *
   * @example
   * ```ts
   * using x = 1;
   * using y =1, z = 2;
   * ```
   */
  declarations: VariableDeclaratorNoInit[];
  declare: true;
  kind: 'let' | 'var';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declarations` | `VariableDeclaratorNoInit[]` | ✗ |  |
| `declare` | `true` | ✗ |  |
| `kind` | `'let' | 'var'` | ✗ |  |

### `LetOrVarNonDeclaredDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface LetOrVarNonDeclaredDeclaration
  extends LetOrConstOrVarDeclarationBase {
  /**
   * In a `let`/`var` declaration, the declarators may have definite assignment
   * assertions or initializers, but not both.
   */
  declarations: (
    | VariableDeclaratorDefiniteAssignment
    | VariableDeclaratorMaybeInit
  )[];
  declare: false;
  kind: 'let' | 'var';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declarations` | `(
    | VariableDeclaratorDefiniteAssignment
    | VariableDeclaratorMaybeInit
  )[]` | ✗ |  |
| `declare` | `false` | ✗ |  |
| `kind` | `'let' | 'var'` | ✗ |  |

### `ConstDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface ConstDeclaration extends LetOrConstOrVarDeclarationBase {
  /**
   * In a `declare const` declaration, the declarators may have initializers, but
   * not definite assignment assertions. Each declarator cannot have both an
   * initializer and a type annotation.
   *
   * Even if the declaration has no `declare`, it may still be ambient and have
   * no initializer.
   */
  declarations: VariableDeclaratorMaybeInit[];
  kind: 'const';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declarations` | `VariableDeclaratorMaybeInit[]` | ✗ |  |
| `kind` | `'const'` | ✗ |  |

### `UsingDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface UsingDeclarationBase extends BaseNode {
  type: AST_NODE_TYPES.VariableDeclaration;
  /**
   * This value will always be `false`
   * because 'declare' modifier cannot appear on a 'using' declaration.
   */
  declare: false;
  /**
   * The keyword used to declare the variable(s)
   * @example
   * ```ts
   * using x = 1;
   * await using y = 2;
   * ```
   */
  kind: 'await using' | 'using';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.VariableDeclaration` | ✗ |  |
| `declare` | `false` | ✗ |  |
| `kind` | `'await using' | 'using'` | ✗ |  |

### `UsingInNormalContextDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface UsingInNormalContextDeclaration extends UsingDeclarationBase {
  /**
   * The variables declared by this declaration.
   * Always non-empty.
   * @example
   * ```ts
   * using x = 1;
   * using y = 1, z = 2;
   * ```
   */
  declarations: UsingInNormalContextDeclarator[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declarations` | `UsingInNormalContextDeclarator[]` | ✗ |  |

### `UsingInForOfDeclaration`

<details><summary>Interface Code</summary>

```ts
export interface UsingInForOfDeclaration extends UsingDeclarationBase {
  /**
   * The variables declared by this declaration.
   * Always has exactly one element.
   * @example
   * ```ts
   * for (using x of y) {}
   * ```
   */
  declarations: [UsingInForOfDeclarator];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `declarations` | `[UsingInForOfDeclarator]` | ✗ |  |


---

## Type Aliases

### `LetOrConstOrVarDeclaration`

```ts
type LetOrConstOrVarDeclaration = | ConstDeclaration
  | LetOrVarDeclaredDeclaration
  | LetOrVarNonDeclaredDeclaration;
```

### `UsingDeclaration`

```ts
type UsingDeclaration = | UsingInForOfDeclaration
  | UsingInNormalContextDeclaration;
```

### `VariableDeclaration`

```ts
type VariableDeclaration = LetOrConstOrVarDeclaration | UsingDeclaration;
```


---