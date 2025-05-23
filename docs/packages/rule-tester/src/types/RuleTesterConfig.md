[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `RuleTesterConfig.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 1
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/RuleTesterConfig.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |
| `DependencyConstraint` | `./DependencyConstraint` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

## Interfaces

### `RuleTesterConfig`

<details><summary>Interface Code</summary>

```ts
export interface RuleTesterConfig extends FlatConfig.Config {
  /**
   * The default filenames to use for type-aware tests.
   * @default { ts: 'file.ts', tsx: 'react.tsx' }
   */
  readonly defaultFilenames?: Readonly<{
    ts: string;
    tsx: string;
  }>;
  /**
   * Constraints that must pass in the current environment for any tests to run.
   */
  readonly dependencyConstraints?: DependencyConstraint;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `defaultFilenames` | `Readonly<{
    ts: string;
    tsx: string;
  }>` | ✓ |  |
| `dependencyConstraints` | `DependencyConstraint` | ✓ |  |


---

## Type Aliases

> No type aliases found in this file.


---