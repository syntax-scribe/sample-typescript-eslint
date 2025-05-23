[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DefinitionBase.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 1
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/DefinitionBase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionType` | `./DefinitionType` |
| `createIdGenerator` | `../ID` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `DefinitionBase`

<details><summary>Class Code</summary>

```ts
export abstract class DefinitionBase<
  Type extends DefinitionType,
  Node extends TSESTree.Node,
  Parent extends TSESTree.Node | null,
  Name extends TSESTree.Node,
> {
  /**
   * A unique ID for this instance - primarily used to help debugging and testing
   */
  public readonly $id: number = generator();

  public readonly type: Type;

  /**
   * The `Identifier` node of this definition
   * @public
   */
  public readonly name: Name;

  /**
   * The enclosing node of the name.
   * @public
   */
  public readonly node: Node;

  /**
   * the enclosing statement node of the identifier.
   * @public
   */
  public readonly parent: Parent;

  constructor(type: Type, name: Name, node: Node, parent: Parent) {
    this.type = type;
    this.name = name;
    this.node = node;
    this.parent = parent;
  }

  /**
   * `true` if the variable is valid in a type context, false otherwise
   */
  public abstract readonly isTypeDefinition: boolean;

  /**
   * `true` if the variable is valid in a value context, false otherwise
   */
  public abstract readonly isVariableDefinition: boolean;
}
```
</details>


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---