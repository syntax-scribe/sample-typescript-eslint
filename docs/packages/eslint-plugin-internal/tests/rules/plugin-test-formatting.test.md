[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `plugin-test-formatting.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 1
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/eslint-plugin-internal/tests/rules/plugin-test-formatting.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `rule` | `../../src/rules/plugin-test-formatting` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Functions

### `wrap(strings: TemplateStringsArray, keys: string[]): string`

<details><summary>Code</summary>

```ts
function wrap(strings: TemplateStringsArray, ...keys: string[]): string {
  const lastIndex = strings.length - 1;
  const code =
    strings.slice(0, lastIndex).reduce((p, s, i) => p + s + keys[i], '') +
    strings[lastIndex];
  return `
ruleTester.run({
  valid: [
    {
      code: ${code},
    },
  ],
});
  `;
}
```
</details>

- **Parameters**:
  - `strings: TemplateStringsArray`
  - `keys: string[]`
- **Return Type**: `string`
- **Calls**:
  - `strings.slice(0, lastIndex).reduce`

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