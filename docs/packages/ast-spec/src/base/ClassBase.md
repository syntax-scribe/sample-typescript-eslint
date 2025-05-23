[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/ast-spec/src/base/ClassBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Identifier` | `../expression/Identifier/spec` |
| `ClassBody` | `../special/ClassBody/spec` |
| `Decorator` | `../special/Decorator/spec` |
| `TSClassImplements` | `../special/TSClassImplements/spec` |
| `TSTypeParameterDeclaration` | `../special/TSTypeParameterDeclaration/spec` |
| `TSTypeParameterInstantiation` | `../special/TSTypeParameterInstantiation/spec` |
| `LeftHandSideExpression` | `../unions/LeftHandSideExpression` |
| `BaseNode` | `./BaseNode` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `ClassBase`

<details><summary>Interface Code</summary>

```ts
export interface ClassBase extends BaseNode {
  /**
   * Whether the class is an abstract class.
   * @example
   * ```ts
   * abstract class Foo {}
   * ```
   */
  abstract: boolean;
  /**
   * The class body.
   */
  body: ClassBody;
  /**
   * Whether the class has been `declare`d:
   * @example
   * ```ts
   * declare class Foo {}
   * ```
   */
  declare: boolean;
  /**
   * The decorators declared for the class.
   * @example
   * ```ts
   * @deco
   * class Foo {}
   * ```
   */
  decorators: Decorator[];
  /**
   * The class's name.
   * - For a `ClassExpression` this may be `null` if the name is omitted.
   * - For a `ClassDeclaration` this may be `null` if and only if the parent is
   *   an `ExportDefaultDeclaration`.
   */
  id: Identifier | null;
  /**
   * The implemented interfaces for the class.
   */
  implements: TSClassImplements[];
  /**
   * The super class this class extends.
   */
  superClass: LeftHandSideExpression | null;
  /**
   * The generic type parameters passed to the superClass.
   */
  superTypeArguments: TSTypeParameterInstantiation | undefined;
  /**
   * The generic type parameters declared for the class.
   */
  typeParameters: TSTypeParameterDeclaration | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `abstract` | `boolean` | ✗ |  |
| `body` | `ClassBody` | ✗ |  |
| `declare` | `boolean` | ✗ |  |
| `decorators` | `Decorator[]` | ✗ |  |
| `id` | `Identifier | null` | ✗ |  |
| `implements` | `TSClassImplements[]` | ✗ |  |
| `superClass` | `LeftHandSideExpression | null` | ✗ |  |
| `superTypeArguments` | `TSTypeParameterInstantiation | undefined` | ✗ |  |
| `typeParameters` | `TSTypeParameterDeclaration | undefined` | ✗ |  |


---

## Type Aliases

> No type aliases found in this file.


---