[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `index.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 3 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 2 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Re-exports](#re-exports)
- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/index.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `InvalidTestCase` | `./InvalidTestCase` |
| `RuleTesterConfig` | `./RuleTesterConfig` |
| `ValidTestCase` | `./ValidTestCase` |


---

## Re-exports

| Type | Source | Exported Names |
|------|--------|----------------|
| named | `./InvalidTestCase` | InvalidTestCase, SuggestionOutput, TestCaseError |
| named | `./RuleTesterConfig` | RuleTesterConfig |
| named | `./ValidTestCase` | TestLanguageOptions, ValidTestCase |


---


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