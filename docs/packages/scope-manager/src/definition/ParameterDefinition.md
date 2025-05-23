[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ParameterDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/ParameterDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `ParameterDefinition`

<details><summary>Class Code</summary>

```ts
export class ParameterDefinition extends DefinitionBase<
  DefinitionType.Parameter,
  | TSESTree.ArrowFunctionExpression
  | TSESTree.FunctionDeclaration
  | TSESTree.FunctionExpression
  | TSESTree.TSCallSignatureDeclaration
  | TSESTree.TSConstructorType
  | TSESTree.TSConstructSignatureDeclaration
  | TSESTree.TSDeclareFunction
  | TSESTree.TSEmptyBodyFunctionExpression
  | TSESTree.TSFunctionType
  | TSESTree.TSMethodSignature,
  null,
  TSESTree.BindingName
> {
  /**
   * Whether the parameter definition is a part of a rest parameter.
   */
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;
  public readonly rest: boolean;

  constructor(
    name: TSESTree.BindingName,
    node: ParameterDefinition['node'],
    rest: boolean,
  ) {
    super(DefinitionType.Parameter, name, node, null);
    this.rest = rest;
  }
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