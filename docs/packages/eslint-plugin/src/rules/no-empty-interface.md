[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-empty-interface.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 4 |
| 📑 Type Aliases | 2 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-empty-interface.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `ScopeType` | `@typescript-eslint/scope-manager` |
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `createRule` | `../util` |
| `isDefinitionFile` | `../util` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `extend` | `any` | const | `node.extends` | ✗ |
| `typeParam` | `string` | let/var | `''` | ✗ |
| `isInAmbientDeclaration` | `any` | const | `isDefinitionFile(context.filename) &&
            scope.type === ScopeType.tsModule &&
            scope.block.declare` | ✗ |
| `useAutoFix` | `boolean` | const | `!(
            isInAmbientDeclaration || mergedWithClassDeclaration
          )` | ✗ |


---

## Functions

### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix => {
            let typeParam = '';
            if (node.typeParameters) {
              typeParam = context.sourceCode.getText(node.typeParameters);
            }
            return fixer.replaceText(
              node,
              `type ${context.sourceCode.getText(
                node.id,
              )}${typeParam} = ${context.sourceCode.getText(extend[0])}`,
            );
          }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `context.sourceCode.getText`
  - `fixer.replaceText`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    allowSingleExtends?: boolean;
  },
];
```

### `MessageIds`

```ts
type MessageIds = 'noEmpty' | 'noEmptyWithSuper';
```


---