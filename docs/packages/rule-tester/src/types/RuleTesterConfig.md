[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `RuleTesterConfig.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📦 Imports | 2 |
| 📐 Interfaces | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/RuleTesterConfig.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `FlatConfig` | `@typescript-eslint/utils/ts-eslint` |
| `DependencyConstraint` | `./DependencyConstraint` |


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