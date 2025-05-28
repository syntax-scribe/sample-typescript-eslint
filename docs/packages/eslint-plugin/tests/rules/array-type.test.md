[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `array-type.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 2 |
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
- [Variables & Constants](#variables-constants)
- [Functions](#functions)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/array-type.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `TSESLint` | `@typescript-eslint/utils` |
| `OptionString` | `../../src/rules/array-type` |
| `rule` | `../../src/rules/array-type` |
| `areOptionsValid` | `../areOptionsValid` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |
| `linter` | `any` | const | `new TSESLint.Linter({ configType: 'eslintrc' })` | ✗ |


---

## Functions

### `testOutput(defaultOption: OptionString, code: string, output: string, readonlyOption: OptionString): void`

<details><summary>Code</summary>

```ts
function testOutput(
      defaultOption: OptionString,
      code: string,
      output: string,
      readonlyOption?: OptionString,
    ): void {
      it(code, () => {
        const result = linter.verifyAndFix(
          code,
          {
            parser: '@typescript-eslint/parser',
            rules: {
              'array-type': [
                2,
                { default: defaultOption, readonly: readonlyOption },
              ],
            },
          },
          {
            fix: true,
          },
        );

        expect(result.messages).toHaveLength(0);
        expect(result.output).toBe(output);
      });
    }
```
</details>

- **Parameters**:
  - `defaultOption: OptionString`
  - `code: string`
  - `output: string`
  - `readonlyOption: OptionString`
- **Return Type**: `void`
- **Calls**:
  - `it`
  - `linter.verifyAndFix`
  - `expect(result.messages).toHaveLength`
  - `expect(result.output).toBe`

---