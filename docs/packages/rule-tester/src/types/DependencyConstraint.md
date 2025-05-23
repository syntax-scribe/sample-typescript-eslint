[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `DependencyConstraint.ts`

## 📚 Table of Contents

- [Interfaces](#interfaces)
- [Type Aliases](#type-aliases)

## 📊 Analysis Summary

- **Functions**: 0
- **Classes**: 0
- **Imports**: 0
- **Interfaces**: 2
- **Type Aliases**: 3

## 🛠️ File Location:
📂 **`packages/rule-tester/src/types/DependencyConstraint.ts`**

## 📦 Imports

> No imports found in this file.


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

> No classes found in this file.


---

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