[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `unbound-method.test.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 6
- **Interfaces**: 0
- **Type Aliases**: 0

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

## Classes

> No classes found in this file.


---

## Interfaces

> No interfaces found in this file.


---

## Type Aliases

> No type aliases found in this file.


---