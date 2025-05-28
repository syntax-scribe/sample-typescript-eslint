[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `unbound-method.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 2 |
| 🧱 Classes | 0 |
| 📦 Imports | 6 |
| 📊 Variables & Constants | 1 |
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
📂 **`packages/eslint-plugin/tests/rules/unbound-method.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `@typescript-eslint/rule-tester` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../src/rules/unbound-method` |
| `Options` | `../../src/rules/unbound-method` |
| `rule` | `../../src/rules/unbound-method` |
| `getFixturesRootDir` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester({
  languageOptions: {
    parserOptions: {
      project: './tsconfig.json',
      tsconfigRootDir: rootPath,
    },
  },
})` | ✗ |


---

## Functions

### `addContainsMethodsClass(code: string): string`

<details><summary>Code</summary>

```ts
function addContainsMethodsClass(code: string): string {
  return `
class ContainsMethods {
  bound?: () => void;
  unbound?(): void;

  static boundStatic?: () => void;
  static unboundStatic?(): void;
}

let instance = new ContainsMethods();

const arith = {
  double(this: void, x: number): number {
    return x * 2;
  }
};

${code}
  `;
}
```
</details>

- **Parameters**:
  - `code: string`
- **Return Type**: `string`
### `addContainsMethodsClassInvalid(code: string[]): InvalidTestCase<MessageIds, Options>[]`

<details><summary>Code</summary>

```ts
function addContainsMethodsClassInvalid(
  code: string[],
): InvalidTestCase<MessageIds, Options>[] {
  return code.map(c => ({
    code: addContainsMethodsClass(c),
    errors: [
      {
        line: 18,
        messageId: 'unboundWithoutThisAnnotation',
      },
    ],
  }));
}
```
</details>

- **Parameters**:
  - `code: string[]`
- **Return Type**: `InvalidTestCase<MessageIds, Options>[]`
- **Calls**:
  - `code.map`
  - `addContainsMethodsClass`

---