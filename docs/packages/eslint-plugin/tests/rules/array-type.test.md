[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `array-type.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 5
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---