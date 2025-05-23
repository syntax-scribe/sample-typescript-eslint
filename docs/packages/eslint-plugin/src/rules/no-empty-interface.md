[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-empty-interface.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 2

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


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