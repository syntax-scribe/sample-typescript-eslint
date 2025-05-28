[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `no-meaningless-void-operator.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 4 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/src/rules/no-meaningless-void-operator.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESLint` | `@typescript-eslint/utils` |
| `TSESTree` | `@typescript-eslint/utils` |
| `ESLintUtils` | `@typescript-eslint/utils` |
| `createRule` | `../util` |


---

## Functions

### `fix(fixer: TSESLint.RuleFixer): TSESLint.RuleFix`

<details><summary>Code</summary>

```ts
(fixer: TSESLint.RuleFixer): TSESLint.RuleFix => {
          return fixer.removeRange([
            context.sourceCode.getTokens(node)[0].range[0],
            context.sourceCode.getTokens(node)[1].range[0],
          ]);
        }
```
</details>

- **Parameters**:
  - `fixer: TSESLint.RuleFixer`
- **Return Type**: `TSESLint.RuleFix`
- **Calls**:
  - `fixer.removeRange`
  - `context.sourceCode.getTokens`

---

## Type Aliases

### `Options`

```ts
type Options = [
  {
    checkNever: boolean;
  },
];
```


---