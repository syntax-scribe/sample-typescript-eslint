[⬅️ Back to Table of Contents](../../../../../index.md)

# 📄 `baseSerializer.ts`

## 📊 Analysis Summary

| Metric | Count |
|--------|-------|
| 🔧 Functions | 1 |
| 🧱 Classes | 0 |
| 📦 Imports | 1 |
| 📊 Variables & Constants | 7 |
| ✨ Decorators | 0 |
| 🔄 Re-exports | 0 |
| ⚡ Async/Await Patterns | 0 |
| 💠 JSX Elements | 0 |
| 🟢 Vue Composition API | 0 |
| 📐 Interfaces | 0 |
| 📑 Type Aliases | 1 |
| 🎯 Enums | 0 |

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