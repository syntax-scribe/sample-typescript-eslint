[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `dependencyConstraints.ts`

## 📚 Table of Contents

- [Imports](#imports)
- [Functions](#functions)

## 📊 Analysis Summary

- **Functions**: 2
- **Classes**: 0
- **Imports**: 2
- **Interfaces**: 0
- **Type Aliases**: 0

## 🛠️ File Location:
📂 **`packages/rule-tester/src/utils/dependencyConstraints.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `DependencyConstraint` | `../types/DependencyConstraint` |
| `SemverVersionConstraint` | `../types/DependencyConstraint` |


---

## Functions

### `satisfiesDependencyConstraint(packageName: string, constraintIn: DependencyConstraint[string]): boolean`

<details><summary>Code</summary>

```ts
function satisfiesDependencyConstraint(
  packageName: string,
  constraintIn: DependencyConstraint[string],
): boolean {
  const constraint: SemverVersionConstraint =
    typeof constraintIn === 'string'
      ? {
          range: `>=${constraintIn}`,
        }
      : constraintIn;

  return semver.satisfies(
    // eslint-disable-next-line @typescript-eslint/no-require-imports
    (require(`${packageName}/package.json`) as { version: string }).version,
    constraint.range,
    typeof constraint.options === 'object'
      ? { ...BASE_SATISFIES_OPTIONS, ...constraint.options }
      : constraint.options,
  );
}
```
</details>

- **Parameters**:
  - `packageName: string`
  - `constraintIn: DependencyConstraint[string]`
- **Return Type**: `boolean`
- **Calls**:
  - `semver.satisfies`
  - `require`
- **Internal Comments**:
```
// eslint-disable-next-line @typescript-eslint/no-require-imports (x2)
```

### `satisfiesAllDependencyConstraints(dependencyConstraints: DependencyConstraint | undefined): boolean`

<details><summary>Code</summary>

```ts
export function satisfiesAllDependencyConstraints(
  dependencyConstraints: DependencyConstraint | undefined,
): boolean {
  if (dependencyConstraints == null) {
    return true;
  }

  for (const [packageName, constraint] of Object.entries(
    dependencyConstraints,
  )) {
    if (!satisfiesDependencyConstraint(packageName, constraint)) {
      return false;
    }
  }

  return true;
}
```
</details>

- **Parameters**:
  - `dependencyConstraints: DependencyConstraint | undefined`
- **Return Type**: `boolean`
- **Calls**:
  - `Object.entries`
  - `satisfiesDependencyConstraint`

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