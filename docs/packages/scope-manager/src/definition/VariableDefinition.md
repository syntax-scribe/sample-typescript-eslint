[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `VariableDefinition.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/definition/VariableDefinition.ts`**

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

### `VariableDefinition`

<details><summary>Class Code</summary>

```ts
export class VariableDefinition extends DefinitionBase<
  DefinitionType.Variable,
  TSESTree.VariableDeclarator,
  TSESTree.VariableDeclaration,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = false;
  public readonly isVariableDefinition = true;

  constructor(
    name: TSESTree.Identifier,
    node: VariableDefinition['node'],
    decl: TSESTree.VariableDeclaration,
  ) {
    super(DefinitionType.Variable, name, node, decl);
  }
}
```
</details>


---