[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `spec.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 7 |
| 📐 Interfaces | 7 |
| 📑 Type Aliases | 4 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/declaration/TSModuleDeclaration/spec.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `../../ast-node-types` |
| `BaseNode` | `../../base/BaseNode` |
| `Identifier` | `../../expression/Identifier/spec` |
| `StringLiteral` | `../../expression/literal/StringLiteral/spec` |
| `TSModuleBlock` | `../../special/TSModuleBlock/spec` |
| `TSQualifiedName` | `../../type/spec` |
| `Literal` | `../../unions/Literal` |


---

## Interfaces

### `TSModuleDeclarationBase`

<details><summary>Interface Code</summary>

```ts
interface TSModuleDeclarationBase extends BaseNode {
  type: AST_NODE_TYPES.TSModuleDeclaration;
  /**
   * The body of the module.
   * This can only be `undefined` for the code `declare module 'mod';`
   */
  body?: TSModuleBlock;
  /**
   * Whether the module is `declare`d
   * @example
   * ```ts
   * declare namespace F {}
   * ```
   */
  declare: boolean;
  // TODO - remove this in the next major (we have `.kind` now)
  /**
   * Whether this is a global declaration
   * @example
   * ```ts
   * declare global {}
   * ```
   *
   * @deprecated Use {@link kind} instead
   */
  global: boolean;
  /**
   * The name of the module
   * ```
   * namespace A {}
   * namespace A.B.C {}
   * module 'a' {}
   * ```
   */
  id: Identifier | Literal | TSQualifiedName;

  /**
   * The keyword used to define this module declaration
   * @example
   * ```ts
   * namespace Foo {}
   * ^^^^^^^^^
   *
   * module 'foo' {}
   * ^^^^^^
   *
   * global {}
   * ^^^^^^
   * ```
   */
  kind: TSModuleDeclarationKind;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `type` | `AST_NODE_TYPES.TSModuleDeclaration` | ✗ |  |
| `body` | `TSModuleBlock` | ✓ |  |
| `declare` | `boolean` | ✗ |  |
| `global` | `boolean` | ✗ |  |
| `id` | `Identifier | Literal | TSQualifiedName` | ✗ |  |
| `kind` | `TSModuleDeclarationKind` | ✗ |  |

### `TSModuleDeclarationNamespace`

<details><summary>Interface Code</summary>

```ts
export interface TSModuleDeclarationNamespace extends TSModuleDeclarationBase {
  body: TSModuleBlock;
  id: Identifier | TSQualifiedName;
  kind: 'namespace';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `body` | `TSModuleBlock` | ✗ |  |
| `id` | `Identifier | TSQualifiedName` | ✗ |  |
| `kind` | `'namespace'` | ✗ |  |

### `TSModuleDeclarationGlobal`

<details><summary>Interface Code</summary>

```ts
export interface TSModuleDeclarationGlobal extends TSModuleDeclarationBase {
  body: TSModuleBlock;
  /**
   * This will always be an Identifier with name `global`
   */
  id: Identifier;
  kind: 'global';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `body` | `TSModuleBlock` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `kind` | `'global'` | ✗ |  |

### `TSModuleDeclarationModuleBase`

<details><summary>Interface Code</summary>

```ts
interface TSModuleDeclarationModuleBase extends TSModuleDeclarationBase {
  kind: 'module';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `kind` | `'module'` | ✗ |  |

### `TSModuleDeclarationModuleWithStringIdNotDeclared`

<details><summary>Interface Code</summary>

```ts
export interface TSModuleDeclarationModuleWithStringIdNotDeclared
  extends TSModuleDeclarationModuleBase {
  body: TSModuleBlock;
  declare: false;
  id: StringLiteral;
  kind: 'module';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `body` | `TSModuleBlock` | ✗ |  |
| `declare` | `false` | ✗ |  |
| `id` | `StringLiteral` | ✗ |  |
| `kind` | `'module'` | ✗ |  |

### `TSModuleDeclarationModuleWithStringIdDeclared`

<details><summary>Interface Code</summary>

```ts
export interface TSModuleDeclarationModuleWithStringIdDeclared
  extends TSModuleDeclarationModuleBase {
  body?: TSModuleBlock;
  declare: true;
  id: StringLiteral;
  kind: 'module';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `body` | `TSModuleBlock` | ✓ |  |
| `declare` | `true` | ✗ |  |
| `id` | `StringLiteral` | ✗ |  |
| `kind` | `'module'` | ✗ |  |

### `TSModuleDeclarationModuleWithIdentifierId`

<details><summary>Interface Code</summary>

```ts
export interface TSModuleDeclarationModuleWithIdentifierId
  extends TSModuleDeclarationModuleBase {
  // Maybe not worth fixing since it's legacy
  body: TSModuleBlock;
  id: Identifier;
  // TODO: we emit the wrong AST for `module A.B {}`
  // https://github.com/typescript-eslint/typescript-eslint/pull/6272 only fixed namespaces
  kind: 'module';
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `body` | `TSModuleBlock` | ✗ |  |
| `id` | `Identifier` | ✗ |  |
| `kind` | `'module'` | ✗ |  |


---

## Type Aliases

### `TSModuleDeclarationKind`

```ts
type TSModuleDeclarationKind = 'global' | 'module' | 'namespace';
```

### `TSModuleDeclarationModuleWithStringId`

```ts
type TSModuleDeclarationModuleWithStringId = | TSModuleDeclarationModuleWithStringIdDeclared
  | TSModuleDeclarationModuleWithStringIdNotDeclared;
```

### `TSModuleDeclarationModule`

```ts
type TSModuleDeclarationModule = | TSModuleDeclarationModuleWithIdentifierId
  | TSModuleDeclarationModuleWithStringId;
```

### `TSModuleDeclaration`

```ts
type TSModuleDeclaration = | TSModuleDeclarationGlobal
  | TSModuleDeclarationModule
  | TSModuleDeclarationNamespace;
```


---