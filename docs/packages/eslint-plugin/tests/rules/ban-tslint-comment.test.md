[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ban-tslint-comment.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📊 Variables & Constants | 3 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/eslint-plugin/tests/rules/ban-tslint-comment.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/ban-tslint-comment` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `PALANTIR_EXAMPLES` | `Testable[]` | const | `[
  { code: '/* tslint:disable */' }, // Disable all rules for the rest of the file
  { code: '/* tslint:enable */' }, // Enable all rules for the rest of the file
  {
    code: '/* tslint:disable:rule1 rule2 rule3... */',
  }, // Disable the listed rules for the rest of the file
  {
    code: '/* tslint:enable:rule1 rule2 rule3... */',
  }, // Enable the listed rules for the rest of the file
  { code: '// tslint:disable-next-line' }, // Disables all rules for the following line
  {
    code: 'someCode(); // tslint:disable-line',
    column: 13,
    output: 'someCode();',
    text: '// tslint:disable-line',
  }, // Disables all rules for the current line
  {
    code: '// tslint:disable-next-line:rule1 rule2 rule3...',
  }, // Disables the listed rules for the next line
]` | ✗ |
| `MORE_EXAMPLES` | `Testable[]` | const | `[
  {
    code: `const woah = doSomeStuff();
// tslint:disable-line
console.log(woah);
`,
    line: 2,
    output: `const woah = doSomeStuff();
console.log(woah);
`,
    text: '// tslint:disable-line',
  },
]` | ✗ |
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |


---

## Interfaces

### `Testable`

<details><summary>Interface Code</summary>

```ts
interface Testable {
  code: string;
  column?: number;
  line?: number;
  output?: string;
  text?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `code` | `string` | ✗ |  |
| `column` | `number` | ✓ |  |
| `line` | `number` | ✓ |  |
| `output` | `string` | ✓ |  |
| `text` | `string` | ✓ |  |


---