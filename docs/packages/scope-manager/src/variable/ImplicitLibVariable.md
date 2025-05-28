[⬅️ Back to Table of Contents](../../../../index.md)

# 📄 `ImplicitLibVariable.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 0 |
| 🧱 Classes | 1 |
| 📦 Imports | 3 |
| 📊 Variables & Constants | 0 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 2 |
| 📑 Type Aliases | 0 |
| 🎯 Enums | 0 |

## 📚 Table of Contents

- [Imports](#imports)
- [Classes](#classes)
- [Interfaces](#interfaces)

## 🛠️ File Location:
📂 **`packages/scope-manager/src/variable/ImplicitLibVariable.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `Scope` | `../scope` |
| `Variable` | `./Variable` |
| `ESLintScopeVariable` | `./ESLintScopeVariable` |


---

## 🔧 Functions

> No functions found in this file.


---

## Classes

### `ImplicitLibVariable`

<details><summary>Class Code</summary>

```ts
export class ImplicitLibVariable
  extends ESLintScopeVariable
  implements Variable
{
  /**
   * `true` if the variable is valid in a type context, false otherwise
   */
  public readonly isTypeVariable: boolean;

  /**
   * `true` if the variable is valid in a value context, false otherwise
   */
  public readonly isValueVariable: boolean;

  public constructor(
    scope: Scope,
    name: string,
    {
      eslintImplicitGlobalSetting,
      isTypeVariable,
      isValueVariable,
      writeable,
    }: ImplicitLibVariableOptions,
  ) {
    super(name, scope);
    this.isTypeVariable = isTypeVariable ?? false;
    this.isValueVariable = isValueVariable ?? false;
    this.writeable = writeable ?? false;
    this.eslintImplicitGlobalSetting =
      eslintImplicitGlobalSetting ?? 'readonly';
  }
}
```
</details>


---

## Interfaces

### `ImplicitLibVariableOptions`

<details><summary>Interface Code</summary>

```ts
export interface ImplicitLibVariableOptions {
  readonly eslintImplicitGlobalSetting?: ESLintScopeVariable['eslintImplicitGlobalSetting'];
  readonly isTypeVariable?: boolean;
  readonly isValueVariable?: boolean;
  readonly writeable?: boolean;
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `eslintImplicitGlobalSetting` | `ESLintScopeVariable['eslintImplicitGlobalSetting']` | ✓ |  |
| `isTypeVariable` | `boolean` | ✓ |  |
| `isValueVariable` | `boolean` | ✓ |  |
| `writeable` | `boolean` | ✓ |  |

### `LibDefinition`

<details><summary>Interface Code</summary>

```ts
export interface LibDefinition {
  libs: readonly LibDefinition[];
  variables: readonly [string, ImplicitLibVariableOptions][];
}
```
</details>

#### Properties

| Name | Type | Optional | Description |
|------|------|----------|-------------|
| `libs` | `readonly LibDefinition[]` | ✗ |  |
| `variables` | `readonly [string, ImplicitLibVariableOptions][]` | ✗ |  |


---