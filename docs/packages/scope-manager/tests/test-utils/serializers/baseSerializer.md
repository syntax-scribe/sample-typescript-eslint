[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `baseSerializer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 7 |
| 📑 Type Aliases | 1 |

## 📚 Table of Contents

- [Imports](#imports)
- [Variables & Constants](#variables-constants)
- [Functions](#functions)
- [Type Aliases](#type-aliases)

## 🛠️ File Location:
📂 **`packages/scope-manager/tests/test-utils/serializers/baseSerializer.ts`**

## 📦 Imports

| Name | Source |
|------|--------|
| `NewPlugin` | `@vitest/pretty-format` |


---

## Variables & Constants

| Name | Type | Kind | Value | Exported |
|------|------|------|-------|----------|
| `SEEN_THINGS` | `Set<unknown>` | const | `new Set<unknown>()` | ✗ |
| `id` | `string` | const | `thing.$id != null ? `$${thing.$id}` : ''` | ✗ |
| `constructorName` | `string` | const | `(Object.getPrototypeOf(thing) as Object)
        .constructor.name` | ✗ |
| `name` | `string` | const | ``${constructorName}${id}`` | ✗ |
| `outputLines` | `any[]` | const | `[]` | ✗ |
| `childIndentation` | `any` | const | `indentation + config.indent` | ✗ |
| `value` | `unknown` | let/var | `thing[key as string]` | ✗ |


---

## Functions

### `createSerializer(type: Constructor, keys: (keyof InstanceType<Constructor>)[]): NewPlugin`

<details><summary>Code</summary>

```ts
export function createSerializer<Constructor extends ConstructorSignature>(
  type: Constructor,
  keys: (keyof InstanceType<Constructor>)[],
): NewPlugin;
```
</details>

- **Parameters**:
  - `type: Constructor`
  - `keys: (keyof InstanceType<Constructor>)[]`
- **Return Type**: `NewPlugin`

---

## Type Aliases

### `ConstructorSignature`

```ts
type ConstructorSignature = new (...args: never) => unknown;
```


---