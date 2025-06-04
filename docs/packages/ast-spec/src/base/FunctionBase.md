[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `FunctionBase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 7 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/FunctionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `TSTypeAnnotation` | `../special/TSTypeAnnotation/spec` |
| `TSTypeParameterDeclaration` | `../special/TSTypeParameterDeclaration/spec` |
| `BlockStatement` | `../statement/BlockStatement/spec` |
| `Expression` | `../unions/Expression` |
| `Parameter` | `../unions/Parameter` |
| `BaseNode` | `./BaseNode` |


---

## Interfaces

### `FunctionBase`

<details><summary>Interface Code</summary>

```ts
export interface FunctionBase extends BaseNode {
  /**
   * Whether the function is async:
   * ```
   * async function foo() {}
   * const x = async function () {}
   * const x = async () => {}
   * ```
   */
  async: boolean;
  /**
   * The body of the function.
   * - For an `ArrowFunctionExpression` this may be an `Expression` or `BlockStatement`.
   * - For a `FunctionDeclaration` or `FunctionExpression` this is always a `BlockStatement`.
   * - For a `TSDeclareFunction` this is always `undefined`.
   * - For a `TSEmptyBodyFunctionExpression` this is always `null`.
   */
  body: BlockStatement | Expression | null | undefined;
  /**
   * This is only `true` if and only if the node is a `TSDeclareFunction` and it has `declare`:
   * ```
   * declare function foo() {}
   * ```
   */
  declare: boolean;
  /**
   * This is only ever `true` if and only the node is an `ArrowFunctionExpression` and the body
   * is an expression:
   * ```
   * (() => 1)
   * ```
   */
  expression: boolean;
  /**
   * Whether the function is a generator function:
   * ```
   * function *foo() {}
   * const x = function *() {}
   * ```
   * This is always `false` for arrow functions as they cannot be generators.
   */
  generator: boolean;
  /**
   * The function's name.
   * - For an `ArrowFunctionExpression` this is always `null`.
   * - For a `FunctionExpression` this may be `null` if the name is omitted.
   * - For a `FunctionDeclaration` or `TSDeclareFunction` this may be `null` if
   *   and only if the parent is an `ExportDefaultDeclaration`.
   */
  id: Identifier | null;
  /**
   * The list of parameters declared for the function.
   */
  params: Parameter[];
  /**
   * The return type annotation for the function.
   */
  returnType: TSTypeAnnotation | undefined;
  /**
   * The generic type parameter declaration for the function.
   */
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `async` | `boolean` | ✗ |  |
| `body` | `BlockStatement | Expression | null | undefined` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `expression` | `boolean` | ✗ |  |
| `generator` | `boolean` | ✗ |  |
| `id` | `Identifier | null` | ✗ |  |
| `params` | `Parameter[]` | ✗ |  |
| `returnType` | `TSTypeAnnotation | undefined` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---