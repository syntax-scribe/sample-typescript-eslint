[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `consistent-type-assertions.test.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 16 |
| 🧱 Classes | 0 |
| 📦 Imports | 7 |
| 📊 Variables & Constants | 9 |
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
📂 **`packages/eslint-plugin/tests/rules/consistent-type-assertions.test.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `TSESTree` | `@typescript-eslint/utils` |
| `RuleTester` | `@typescript-eslint/rule-tester` |
| `MessageIds` | `../../src/rules/consistent-type-assertions` |
| `Options` | `../../src/rules/consistent-type-assertions` |
| `rule` | `../../src/rules/consistent-type-assertions` |
| `dedupeTestCases` | `../dedupeTestCases` |
| `batchedSingleLineTests` | `../RuleTester` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `ruleTester` | `any` | const | `new RuleTester()` | ✗ |
| `ANGLE_BRACKET_TESTS_EXCEPT_CONST_CASE` | `"\nconst x = <Foo>new Generic<int>();\nconst x = <A>b;\nconst x = <readonly number[]>[1];\nconst x = <a | b>('string');\nconst x = <A>!'string';\nconst x = <A>a + b;\nconst x = <(A)>a + (b);\nconst x = <Foo>(new Generic<string>());\nconst x = new (<Foo>Generic<string>)();\nconst x = new (<Foo>Generic<string>)('strin...` | const | ``
const x = <Foo>new Generic<int>();
const x = <A>b;
const x = <readonly number[]>[1];
const x = <a | b>('string');
const x = <A>!'string';
const x = <A>a + b;
const x = <(A)>a + (b);
const x = <Foo>(new Generic<string>());
const x = new (<Foo>Generic<string>)();
const x = new (<Foo>Generic<string>)('string');
const x = () => <Foo>{ bar: 5 };
const x = () => <Foo>({ bar: 5 });
const x = () => <Foo>bar;
const x = <Foo>bar<string>\`\${"baz"}\`;`` | ✗ |
| `ANGLE_BRACKET_TESTS` | `"\nconst x = <Foo>new Generic<int>();\nconst x = <A>b;\nconst x = <readonly number[]>[1];\nconst x = <a | b>('string');\nconst x = <A>!'string';\nconst x = <A>a + b;\nconst x = <(A)>a + (b);\nconst x = <Foo>(new Generic<string>());\nconst x = new (<Foo>Generic<string>)();\nconst x = new (<Foo>Generic<string>)('strin...` | const | ``${ANGLE_BRACKET_TESTS_EXCEPT_CONST_CASE}
const x = <const>{ key: 'value' };
`` | ✗ |
| `AS_TESTS_EXCEPT_CONST_CASE` | `"\nconst x = new Generic<int>() as Foo;\nconst x = b as A;\nconst x = [1] as readonly number[];\nconst x = 'string' as a | b;\nconst x = !'string' as A;\nconst x = (a as A) + b;\nconst x = (a as A) + (b);\nconst x = new Generic<string>() as Foo;\nconst x = new ((Generic<string>) as Foo)();\nconst x = new ((Generic<s...` | const | ``
const x = new Generic<int>() as Foo;
const x = b as A;
const x = [1] as readonly number[];
const x = 'string' as a | b;
const x = !'string' as A;
const x = (a as A) + b;
const x = (a as A) + (b);
const x = new Generic<string>() as Foo;
const x = new ((Generic<string>) as Foo)();
const x = new ((Generic<string>) as Foo)('string');
const x = () => ({ bar: 5 } as Foo);
const x = () => ({ bar: 5 } as Foo);
const x = () => (bar as Foo);
const x = bar<string>\`\${"baz"}\` as Foo;`` | ✗ |
| `AS_TESTS` | `"\nconst x = new Generic<int>() as Foo;\nconst x = b as A;\nconst x = [1] as readonly number[];\nconst x = 'string' as a | b;\nconst x = !'string' as A;\nconst x = (a as A) + b;\nconst x = (a as A) + (b);\nconst x = new Generic<string>() as Foo;\nconst x = new ((Generic<string>) as Foo)();\nconst x = new ((Generic<s...` | const | ``${AS_TESTS_EXCEPT_CONST_CASE}
const x = { key: 'value' } as const;
`` | ✗ |
| `OBJECT_LITERAL_AS_CASTS` | `"\nconst x = {} as Foo<int>;\nconst x = ({}) as a | b;\nconst x = {} as A + b;\n"` | const | ``
const x = {} as Foo<int>;
const x = ({}) as a | b;
const x = {} as A + b;
`` | ✗ |
| `OBJECT_LITERAL_ANGLE_BRACKET_CASTS` | `"\nconst x = <Foo<int>>{};\nconst x = <a | b>({});\nconst x = <A>{} + b;\n"` | const | ``
const x = <Foo<int>>{};
const x = <a | b>({});
const x = <A>{} + b;
`` | ✗ |
| `OBJECT_LITERAL_ARGUMENT_AS_CASTS` | `"\nprint({ bar: 5 } as Foo)\nnew print({ bar: 5 } as Foo)\nfunction foo() { throw { bar: 5 } as Foo }\nfunction b(x = {} as Foo.Bar) {}\nfunction c(x = {} as Foo) {}\nprint?.({ bar: 5 } as Foo)\nprint?.call({ bar: 5 } as Foo)\nprint`${{ bar: 5 } as Foo}`\n"` | const | ``
print({ bar: 5 } as Foo)
new print({ bar: 5 } as Foo)
function foo() { throw { bar: 5 } as Foo }
function b(x = {} as Foo.Bar) {}
function c(x = {} as Foo) {}
print?.({ bar: 5 } as Foo)
print?.call({ bar: 5 } as Foo)
print\`\${{ bar: 5 } as Foo}\`
`` | ✗ |
| `OBJECT_LITERAL_ARGUMENT_ANGLE_BRACKET_CASTS` | `"\nprint(<Foo>{ bar: 5 })\nnew print(<Foo>{ bar: 5 })\nfunction foo() { throw <Foo>{ bar: 5 } }\nprint?.(<Foo>{ bar: 5 })\nprint?.call(<Foo>{ bar: 5 })\nprint`${<Foo>{ bar: 5 }}`\n"` | const | ``
print(<Foo>{ bar: 5 })
new print(<Foo>{ bar: 5 })
function foo() { throw <Foo>{ bar: 5 } }
print?.(<Foo>{ bar: 5 })
print?.call(<Foo>{ bar: 5 })
print\`\${<Foo>{ bar: 5 }}\`
`` | ✗ |


---

## Functions

### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`
### `parse(): TSESTree.Program`

<details><summary>Code</summary>

```ts
(): TSESTree.Program => parser.parse('123;')
```
</details>

- **Return Type**: `TSESTree.Program`
- **Calls**:
  - `parser.parse`

---