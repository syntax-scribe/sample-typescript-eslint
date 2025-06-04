[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ClassNameDefinition.ts`

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
📂 **`packages/scope-manager/src/definition/ClassNameDefinition.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `DefinitionBase` | `./DefinitionBase` |
| `DefinitionType` | `./DefinitionType` |


---


---

## Classes

### `ClassNameDefinition`

<details><summary>Class Code</summary>

```ts
export class ClassNameDefinition extends DefinitionBase<
  DefinitionType.ClassName,
  TSESTree.ClassDeclaration | TSESTree.ClassExpression,
  null,
  TSESTree.Identifier
> {
  public readonly isTypeDefinition = true;
  public readonly isVariableDefinition = true;

  constructor(name: TSESTree.Identifier, node: ClassNameDefinition['node']) {
    super(DefinitionType.ClassName, name, node, null);
  }
}
```
</details>


---