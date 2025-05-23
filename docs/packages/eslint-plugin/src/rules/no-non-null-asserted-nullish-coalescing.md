[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-non-null-asserted-nullish-coalescing.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 8
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-non-null-asserted-nullish-coalescing.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Definition` | `@typescript-eslint/scope-manager` |
| `TSESLint` | `@typescript-eslint/utils` |
| `DefinitionType` | `@typescript-eslint/scope-manager` |
| `ASTUtils` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `nullThrows` | `../util` |
| `NullThrowsReasons` | `../util` |


---

## Functions

### `hasAssignmentBeforeNode(variable: TSESLint.Scope.Variable, node: TSESTree.Node): boolean`

<details><summary>Code</summary>

```ts
function hasAssignmentBeforeNode(
  variable: TSESLint.Scope.Variable,
  node: TSESTree.Node,
): boolean {
  return (
    variable.references.some(
      ref => ref.isWrite() && ref.identifier.range[1] < node.range[1],
    ) ||
    variable.defs.some(
      def =>
        isDefinitionWithAssignment(def) && def.node.range[1] < node.range[1],
    )
  );
}
```
</details>

- **Parameters**:
  - `variable: TSESLint.Scope.Variable`
  - `node: TSESTree.Node`
- **Return Type**: `boolean`
- **Calls**:
  - `variable.references.some`
  - `ref.isWrite`
  - `variable.defs.some`
  - `isDefinitionWithAssignment`
### `isDefinitionWithAssignment(definition: Definition): boolean`

<details><summary>Code</summary>

```ts
function isDefinitionWithAssignment(definition: Definition): boolean {
  if (definition.type !== DefinitionType.Variable) {
    return false;
  }

  const variableDeclarator = definition.node;
  return variableDeclarator.definite || variableDeclarator.init != null;
}
```
</details>

- **Parameters**:
  - `definition: Definition`
- **Return Type**: `boolean`

---

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---