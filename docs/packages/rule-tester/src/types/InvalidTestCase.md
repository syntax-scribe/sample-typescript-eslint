[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `InvalidTestCase.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 0 |
| 📦 Imports | 5 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 3 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/InvalidTestCase.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `AST_NODE_TYPES` | `@typescript-eslint/utils` |
| `AST_TOKEN_TYPES` | `@typescript-eslint/utils` |
| `ReportDescriptorMessageData` | `@typescript-eslint/utils/ts-eslint` |
| `DependencyConstraint` | `./DependencyConstraint` |
| `ValidTestCase` | `./ValidTestCase` |


---


---

## Interfaces

### `SuggestionOutput<MessageIds extends string>`

<details><summary>Interface Code</summary>

```ts
export interface SuggestionOutput<MessageIds extends string> {
  /**
   * The data used to fill the message template.
   */
  readonly data?: ReportDescriptorMessageData;
  /**
   * Reported message ID.
   */
  readonly messageId: MessageIds;
  /**
   * NOTE: Suggestions will be applied as a stand-alone change, without triggering multi-pass fixes.
   * Each individual error has its own suggestion, so you have to show the correct, _isolated_ output for each suggestion.
   */
  readonly output: string;

  // we disallow this because it's much better to use messageIds for reusable errors that are easily testable
  // readonly desc?: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `data` | `ReportDescriptorMessageData` | ✓ |  |
| `messageId` | `MessageIds` | ✗ |  |
| `output` | `string` | ✗ |  |

### `TestCaseError<MessageIds extends string>`

<details><summary>Interface Code</summary>

```ts
export interface TestCaseError<MessageIds extends string> {
  /**
   * The 1-based column number of the reported start location.
   */
  readonly column?: number;
  /**
   * The data used to fill the message template.
   */
  readonly data?: ReportDescriptorMessageData;
  /**
   * The 1-based column number of the reported end location.
   */
  readonly endColumn?: number;
  /**
   * The 1-based line number of the reported end location.
   */
  readonly endLine?: number;
  /**
   * The 1-based line number of the reported start location.
   */
  readonly line?: number;
  /**
   * Reported message ID.
   */
  readonly messageId: MessageIds;
  /**
   * Reported suggestions.
   */
  readonly suggestions?: readonly SuggestionOutput<MessageIds>[] | null;
  /**
   * The type of the reported AST node.
   */
  readonly type?: AST_NODE_TYPES | AST_TOKEN_TYPES;

  // we disallow this because it's much better to use messageIds for reusable errors that are easily testable
  // readonly message?: string | RegExp;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `column` | `number` | ✓ |  |
| `data` | `ReportDescriptorMessageData` | ✓ |  |
| `endColumn` | `number` | ✓ |  |
| `endLine` | `number` | ✓ |  |
| `line` | `number` | ✓ |  |
| `messageId` | `MessageIds` | ✗ |  |
| `suggestions` | `readonly SuggestionOutput<MessageIds>[] | null` | ✓ |  |
| `type` | `AST_NODE_TYPES | AST_TOKEN_TYPES` | ✓ |  |

### `InvalidTestCase<MessageIds extends string, Options extends readonly unknown[]>`

<details><summary>Interface Code</summary>

```ts
export interface InvalidTestCase<
  MessageIds extends string,
  Options extends readonly unknown[],
> extends ValidTestCase<Options> {
  /**
   * Constraints that must pass in the current environment for the test to run
   */
  readonly dependencyConstraints?: DependencyConstraint;
  /**
   * Expected errors.
   */
  readonly errors: readonly TestCaseError<MessageIds>[];
  /**
   * The expected code after autofixes are applied. If set to `null`, the test runner will assert that no autofix is suggested.
   */
  readonly output?: string | string[] | null;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `dependencyConstraints` | `DependencyConstraint` | ✓ |  |
| `errors` | `readonly TestCaseError<MessageIds>[]` | ✗ |  |
| `output` | `string | string[] | null` | ✓ |  |


---