[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 3
- **Interfaces**: 2
- **Type Aliases**: 2

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `./InvalidTestCase` |
| `RuleTesterConfig` | `./RuleTesterConfig` |
| `ValidTestCase` | `./ValidTestCase` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `RunTests<MessageIds extends string, Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface RunTests<
  MessageIds extends string,
  Options extends readonly unknown[],
> {
  readonly invalid: readonly InvalidTestCase<MessageIds, Options>[];
  // RuleTester.run also accepts strings for valid cases
  readonly valid: readonly (string | ValidTestCase<Options>)[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `invalid` | `readonly InvalidTestCase<MessageIds, Options>[]` | ✗ |  |
| `valid` | `readonly (string | ValidTestCase<Options>)[]` | ✗ |  |

### `NormalizedRunTests<MessageIds extends string, Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface NormalizedRunTests<
  MessageIds extends string,
  Options extends readonly unknown[],
> {
  readonly invalid: readonly InvalidTestCase<MessageIds, Options>[];
  readonly valid: readonly ValidTestCase<Options>[];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `invalid` | `readonly InvalidTestCase<MessageIds, Options>[]` | ✗ |  |
| `valid` | `readonly ValidTestCase<Options>[]` | ✗ |  |


---

## Type Aliases

### `Mutable<T>`

```ts
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};
```

### `TesterConfigWithDefaults`

```ts
type TesterConfigWithDefaults = Mutable<
  Required<
    Pick<RuleTesterConfig, 'defaultFilenames' | 'languageOptions' | 'rules'>
  > &
    RuleTesterConfig
>;
```


---