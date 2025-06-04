[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ESLintScopeVariable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 2 |
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
📂 **`packages/scope-manager/src/variable/ESLintScopeVariable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/types` |
| `VariableBase` | `./VariableBase` |


---


---

## Classes

### `ESLintScopeVariable`

<details><summary>Class Code</summary>

```ts
export class ESLintScopeVariable extends VariableBase {
  /**
   * Written to by ESLint.
   * If this key exists, this variable is a global variable added by ESLint.
   * If this is `true`, this variable can be assigned arbitrary values.
   * If this is `false`, this variable is readonly.
   */
  public writeable?: boolean; // note that this isn't a typo - ESlint uses this spelling here

  /**
   * Written to by ESLint.
   * This property is undefined if there are no globals directive comments.
   * The array of globals directive comments which defined this global variable in the source code file.
   */
  public eslintExplicitGlobal?: boolean;

  /**
   * Written to by ESLint.
   * The configured value in config files. This can be different from `variable.writeable` if there are globals directive comments.
   */
  public eslintImplicitGlobalSetting?: 'readonly' | 'writable';

  /**
   * Written to by ESLint.
   * If this key exists, it is a global variable added by ESLint.
   * If `true`, this global variable was defined by a globals directive comment in the source code file.
   */
  public eslintExplicitGlobalComments?: TSESTree.Comment[];
}
```
</details>


---