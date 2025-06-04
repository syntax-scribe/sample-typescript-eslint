[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DependencyConstraint.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 3 |

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/DependencyConstraint.ts`**

## Interfaces

### `RangeOptions`

<details><summary>Interface Code</summary>

```ts
export interface RangeOptions {
  includePrerelease?: boolean | undefined;
  loose?: boolean | undefined;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `includePrerelease` | `boolean | undefined` | ✓ |  |
| `loose` | `boolean | undefined` | ✓ |  |

### `SemverVersionConstraint`

<details><summary>Interface Code</summary>

```ts
export interface SemverVersionConstraint {
  readonly options?: boolean | RangeOptions;
  readonly range: string;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `options` | `boolean | RangeOptions` | ✓ |  |
| `range` | `string` | ✗ |  |


---

## Type Aliases

### `AtLeastVersionConstraint`

```ts
type AtLeastVersionConstraint = | `${number}.${number}.${number}-${string}`
  | `${number}.${number}.${number}`
  | `${number}.${number}`
  | `${number}`;
```

### `VersionConstraint`

```ts
type VersionConstraint = | AtLeastVersionConstraint
  | SemverVersionConstraint;
```

### `DependencyConstraint`

/**
 * Passing a string for the value is shorthand for a '>=' constraint
 */

```ts
type DependencyConstraint = Readonly<Record<string, VersionConstraint>>;
```


---